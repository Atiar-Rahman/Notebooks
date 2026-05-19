```jsx
import { useState } from "react";
import { Link, useParams } from "react-router-dom";

const Products = () => {

    const products = [
        {
            id: 1,
            category: 1,
            name: "Product 1",
            price: 100,
        },
        {
            id: 2,
            category: 1,
            name: "Product 2",
            price: 200,
        },
        {
            id: 3,
            category: 2,
            name: "Product 3",
            price: 300,
        },
    ];

    const { category_id } = useParams();

    // selected product for edit
    const [selectedProduct, setSelectedProduct] = useState(null);

    // filter category products
    const categoryProducts = products.filter(
        (product) => product.category === Number(category_id)
    );

    // open modal
    const openModal = (product = null) => {

        setSelectedProduct(product);

        document.getElementById("my_modal_3").showModal();
    };

    // submit form
    const handleSubmit = (e) => {

        e.preventDefault();

        const form = e.target;

        const name = form.name.value;
        const price = form.price.value;

        const data = {
            id: selectedProduct?.id || Date.now(),
            category: Number(category_id),
            name,
            price,
        };

        // EDIT
        if (selectedProduct) {

            console.log("Updated Product:", data);

        }

        // ADD
        else {

            console.log("New Product:", data);

        }

        form.reset();

        document.getElementById("my_modal_3").close();
    };

    return (
        <div className="text-black">

            {/* HEADER */}
            <div className="flex justify-between items-center mb-6 border p-4 rounded">

                <h2 className="text-2xl font-bold">
                    Products
                </h2>

                <button
                    className="
                        bg-blue-500
                        text-white
                        px-4
                        py-2
                        rounded
                        cursor-pointer
                    "
                    onClick={() => openModal()}
                >
                    Add Product
                </button>

            </div>

            {/* PRODUCT GRID */}
            <div className="
                grid
                grid-cols-1
                md:grid-cols-2
                lg:grid-cols-3
                gap-4
            ">

                {categoryProducts.map((product) => (

                    <div
                        key={product.id}
                        className="
                            border
                            p-4
                            bg-gray-100
                            rounded
                            shadow
                        "
                    >

                        <h1 className="text-xl font-semibold">
                            {product.name}
                        </h1>

                        <p className="mt-2">
                            Price: ${product.price}
                        </p>

                        {/* ACTION BUTTONS */}
                        <div className="flex flex-wrap gap-2 mt-4">

                            <Link
                                className="
                                    bg-blue-100
                                    px-4
                                    py-2
                                    rounded
                                "
                                to={`/dashboard/category/${category_id}/products/${product.id}`}
                            >
                                View
                            </Link>

                            <button
                                className="
                                    bg-green-100
                                    px-4
                                    py-2
                                    rounded
                                    cursor-pointer
                                "
                                onClick={() => openModal(product)}
                            >
                                Edit
                            </button>

                            <Link
                                className="
                                    bg-yellow-100
                                    px-4
                                    py-2
                                    rounded
                                "
                                to={`/dashboard/category/${category_id}/products/${product.id}/images`}
                            >
                                Images
                            </Link>

                            <button
                                className="
                                    bg-red-100
                                    px-4
                                    py-2
                                    rounded
                                    cursor-pointer
                                "
                            >
                                Delete
                            </button>

                        </div>

                    </div>

                ))}

            </div>

            {/* MODAL */}
            <dialog id="my_modal_3" className="modal">

                <div className="modal-box">

                    {/* CLOSE BUTTON */}
                    <form method="dialog">

                        <button
                            className="
                                btn
                                btn-sm
                                btn-circle
                                btn-ghost
                                absolute
                                right-2
                                top-2
                            "
                        >
                            ✕
                        </button>

                    </form>

                    {/* TITLE */}
                    <h2 className="text-2xl font-bold mb-4">

                        {
                            selectedProduct
                                ? "Edit Product"
                                : "Add Product"
                        }

                    </h2>

                    {/* FORM */}
                    <form
                        onSubmit={handleSubmit}
                        className="flex flex-col gap-4"
                    >

                        <input
                            type="text"
                            name="name"
                            placeholder="Product Name"
                            defaultValue={selectedProduct?.name || ""}
                            className="
                                border
                                p-2
                                rounded
                            "
                        />

                        <input
                            type="number"
                            name="price"
                            placeholder="Product Price"
                            defaultValue={selectedProduct?.price || ""}
                            className="
                                border
                                p-2
                                rounded
                            "
                        />

                        <button
                            type="submit"
                            className="
                                bg-green-500
                                text-white
                                py-2
                                px-4
                                rounded
                                cursor-pointer
                            "
                        >

                            {
                                selectedProduct
                                    ? "Update Product"
                                    : "Add Product"
                            }

                        </button>

                    </form>

                </div>

            </dialog>

        </div>
    );
};

export default Products;
```

