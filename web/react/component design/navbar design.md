```jsx
import React from "react";

const Navbar = () => {
  const navlinks = (
    <>
      <li>
        <a className="active bg-primary text-white rounded-lg">Home</a>
      </li>

      {/* Products Dropdown */}
      <li>
        <details>
          <summary className="font-medium">Products</summary>

          <ul className="p-2 bg-base-100 rounded-xl shadow-xl w-60">
            <li>
              <a className="hover:bg-primary hover:text-white">📱 Mobile</a>
            </li>

            <li>
              <a className="hover:bg-primary hover:text-white">💻 Laptop</a>
            </li>

            <li>
              <a className="hover:bg-primary hover:text-white">
                🎧 Accessories
              </a>
            </li>
          </ul>
        </details>
      </li>

      {/* Services Dropdown */}
      <li>
        <details>
          <summary className="font-medium">Services</summary>

          <ul className="p-2 bg-base-100 rounded-xl shadow-xl w-64">
            <li>
              <details>
                <summary>Software Development</summary>

                <ul className="bg-base-200 rounded-lg p-2">
                  <li>
                    <a>🌐 Web Development</a>
                  </li>

                  <li>
                    <a>📱 App Development</a>
                  </li>

                  <li>
                    <a>🔌 API Development</a>
                  </li>

                  <li>
                    <a>⚙ Other</a>
                  </li>
                </ul>
              </details>
            </li>

            <li>
              <a>🎨 UI/UX Design</a>
            </li>

            <li>
              <a>🚀 SEO</a>
            </li>
          </ul>
        </details>
      </li>

      {/* Category */}

      <li>
        <details>
          <summary>Categories</summary>

          <ul className="p-2 bg-base-100 rounded-xl shadow-xl w-52">
            <li>
              <a>🎧 Headset</a>
            </li>

            <li>
              <a>⌚ Hand Watch</a>
            </li>

            <li>
              <a>🕒 Wall Watch</a>
            </li>
          </ul>
        </details>
      </li>

      <li>
        <a>About</a>
      </li>

      <li>
        <a>Contact</a>
      </li>
    </>
  );

  return (
    <div className="navbar bg-base-100 shadow-lg sticky top-0 z-50 px-4">
      {/* Logo */}

      <div className="navbar-start">
        <div className="dropdown">
          <div tabIndex={0} role="button" className="btn btn-ghost lg:hidden">
            ☰
          </div>

          <ul
            tabIndex={0}
            className="
            menu menu-sm 
            dropdown-content 
            bg-base-100 
            rounded-xl 
            mt-3 
            w-64 
            p-3 
            shadow-xl
            "
          >
            {navlinks}
          </ul>
        </div>

        <a
          className="
          text-2xl 
          font-bold 
          bg-linear-to-r 
          from-primary 
          to-secondary 
          bg-clip-text 
          text-transparent
        "
        >
          MyStore
        </a>
      </div>

      {/* Desktop Menu */}

      <div className="navbar-center hidden lg:flex">
        <ul
          className="
          menu 
          menu-horizontal 
          gap-2
          font-medium
        "
        >
          {navlinks}
        </ul>
      </div>

      {/* Right Side */}

      <div className="navbar-end gap-3">
        <button className="btn btn-outline btn-primary">Login</button>

        <button className="btn btn-primary">Sign Up</button>
      </div>
    </div>
  );
};

export default Navbar;

```

