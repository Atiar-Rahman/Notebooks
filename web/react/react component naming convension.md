

React-এ **component name choose করার মূল rule** হলো: নাম দেখেই যেন বোঝা যায় component-টা কী কাজ করে বা কী UI represent করে।

### 1. Component name সবসময় `PascalCase`

```jsx
function ProductCard() {
  return <div>Product</div>;
}
```

✅ `ProductCard`  
❌ `productCard`  
❌ `product_card`

---

### 2. UI element হলে noun-based name

যদি component একটা নির্দিষ্ট UI অংশ হয়:

```text
Button
Input
Modal
Navbar
Sidebar
Footer
ProductCard
ProductList
ProductImage
```

Example:

```jsx
function ProductCard() {
  return (
    <div>
      <h2>iPhone 15</h2>
      <p>$800</p>
    </div>
  );
}
```

---

### 3. কোনো page হলে `Page` suffix ব্যবহার করতে পারো

```text
HomePage
ProductPage
ProductDetailsPage
LoginPage
RegisterPage
DashboardPage
ProfilePage
```

```jsx
function ProductDetailsPage() {
  return <div>Product Details</div>;
}
```

---

### 4. Layout হলে `Layout` suffix

```text
DashboardLayout
AuthLayout
AdminLayout
MainLayout
ShopLayout
```

```jsx
function DashboardLayout({ children }) {
  return (
    <div>
      <Sidebar />
      <main>{children}</main>
    </div>
  );
}
```

---

### 5. কোনো feature-এর অংশ হলে feature + responsibility

ধরো e-commerce:

```text
ProductCard
ProductList
ProductFilter
ProductSearch
ProductForm
ProductDetails
ProductReview
ProductReviewList
```

এখানে নাম দেখেই বোঝা যাচ্ছে কোন component কী করছে।

---

### 6. খুব generic নাম avoid করো

❌ এগুলো:

```text
Box
Container
Component1
Data
Section
MyComponent
Test
NewComponent
```

এগুলো দেখে component-এর উদ্দেশ্য বোঝা যায় না।

এর পরিবর্তে:

```text
ProductFilter
OrderSummary
UserProfile
PaymentForm
CartSummary
ReviewList
```

---

### 7. একই ধরনের component হলে consistent naming রাখো

ধরো তোমার project:

```text
components/
├── product/
│   ├── ProductCard.jsx
│   ├── ProductList.jsx
│   ├── ProductFilter.jsx
│   └── ProductForm.jsx
│
├── order/
│   ├── OrderCard.jsx
│   ├── OrderList.jsx
│   ├── OrderSummary.jsx
│   └── OrderStatus.jsx
│
└── user/
    ├── UserCard.jsx
    ├── UserList.jsx
    └── UserProfile.jsx
```

এটা অনেক clean approach।

### একটা সহজ formula মনে রাখো

**`[What] + [Purpose]`**

যেমন:

```text
Product + Card       → ProductCard
Product + Filter     → ProductFilter
Order + Summary      → OrderSummary
Order + Status       → OrderStatus
User + Profile       → UserProfile
Payment + Form       → PaymentForm
```

আর **Page / Layout** হলে:

```text
ProductPage
DashboardPage
AuthLayout
DashboardLayout
```

সবচেয়ে গুরুত্বপূর্ণ হলো **একটা naming convention বেছে নিয়ে পুরো project-এ সেটাই follow করা**।

----
# যা। E-commerce-এ `ProductCard`, `OrderSummary` এভাবে নাম দেওয়া সহজ। কিন্তু **hotel, hospital, job portal, university, logistics**—এগুলোতে component naming কীভাবে করবে, সেটা বুঝতে হলে একটা common system দরকার।

আমি সাধারণত এই rule follow করতে বলব:

## 1. প্রথমে Domain/Feature চিন্তা করো

ধরো Hotel Management:

```text
hotel/
├── HotelCard
├── HotelList
├── HotelForm
├── RoomCard
├── RoomList
├── RoomForm
├── BookingCard
├── BookingForm
└── BookingSummary
```

এখানে প্রতিটি component-এর নাম:

> **Entity + কাজ**

---

## 2. Hospital Project

ধরো:

```text
Patient
Doctor
Appointment
Prescription
Medicine
Invoice
```

তাহলে:

```text
PatientCard
PatientForm
PatientList

DoctorCard
DoctorProfile
DoctorList

AppointmentCard
AppointmentForm
AppointmentList
AppointmentDetails

PrescriptionForm
PrescriptionDetails

MedicineCard
MedicineList

InvoiceCard
InvoiceDetails
PaymentForm
```

এখানে `Card`, `Form`, `List`, `Details` এগুলো **component-এর responsibility** বোঝাচ্ছে।

---

## 3. Job Portal

Entities:

```text
Job
Company
Applicant
Application
Resume
Interview
```

Components:

```text
JobCard
JobList
JobSearch
JobFilter
JobDetails
JobForm

CompanyCard
CompanyProfile
CompanyList

ApplicantProfile
ApplicantList

ApplicationCard
ApplicationList
ApplicationStatus

ResumeCard
ResumePreview
ResumeUpload

InterviewCard
InterviewSchedule
InterviewDetails
```

---

## 4. Hotel Project

এখানে একটা গুরুত্বপূর্ণ ব্যাপার আছে।

ধরো:

```text
Hotel
Room
Booking
Guest
Payment
Review
```

তাহলে:

```text
HotelCard
HotelList
HotelDetails

RoomCard
RoomList
RoomDetails
RoomAvailability

BookingCard
BookingList
BookingForm
BookingDetails
BookingSummary

GuestProfile

PaymentForm
PaymentDetails

ReviewCard
ReviewList
ReviewForm
```

---

# 5. কিন্তু সব component Entity + Purpose হবে না

কিছু component **shared/common** হবে।

যেমন:

```text
Button
Input
Select
Modal
Table
Pagination
Loader
Spinner
Dropdown
Badge
Alert
ConfirmDialog
```

এগুলো কোনো নির্দিষ্ট domain-এর না।

তাই project-এ:

```text
components/
├── ui/
│   ├── Button.jsx
│   ├── Input.jsx
│   ├── Modal.jsx
│   ├── Table.jsx
│   └── Pagination.jsx
│
├── hotel/
│   ├── HotelCard.jsx
│   ├── HotelList.jsx
│   └── HotelDetails.jsx
│
├── room/
│   ├── RoomCard.jsx
│   ├── RoomList.jsx
│   └── RoomAvailability.jsx
│
└── booking/
    ├── BookingCard.jsx
    ├── BookingForm.jsx
    └── BookingDetails.jsx
```

এটা অনেক scalable।

---

# 6. Dashboard-এর component হলে?

এখানে একটু আলাদা naming করতে পারো।

```text
DashboardLayout
DashboardSidebar
DashboardNavbar
DashboardHeader
DashboardStats
DashboardOverview
```

কিন্তু যদি sidebar পুরো application-এ reuse হয়:

```text
Sidebar
Navbar
Header
```

তাহলে `Dashboard` prefix দরকার নেই।

---

# 7. Complex component হলে নাম দেখে কাজ বোঝা উচিত

ধরো hotel booking page-এ:

```text
BookingForm
```

এর ভিতরে অনেক কিছু আছে।

তখন ভেঙে দিতে পারো:

```text
BookingForm
├── GuestInformation
├── RoomSelection
├── BookingDatePicker
├── PaymentMethod
└── BookingSummary
```

এখানে:

```text
GuestInformation
RoomSelection
BookingDatePicker
PaymentMethod
BookingSummary
```

এগুলোও valid component name।

---

# 8. `Section` কখন ব্যবহার করবে?

ধরো homepage:

```text
HeroSection
FeaturedHotelsSection
PopularRoomsSection
TestimonialsSection
NewsletterSection
```

এখানে `Section` useful কারণ এগুলো সত্যিই page-এর section।

কিন্তু:

```text
ProductSection
UserSection
```

এভাবে শুধু generic করে ফেলো না, যদি আরও meaningful নাম দেওয়া যায়।

---

# 9. `Manager`, `Container`, `Wrapper` নিয়ে সাবধান

Beginner হিসেবে অনেক সময় এমন নাম দেওয়া হয়:

```text
ProductContainer
UserContainer
BookingContainer
```

শুধু নামটা শুনে বোঝা যায় না component কী করছে।

যদি data fetch করে:

```text
ProductListContainer
```

বা modern React architecture-এ আরও ভালোভাবে:

```text
ProductList
```

আর fetching logic আলাদা hook/service-এ রাখা যায়।

---

# 10. সবচেয়ে useful naming formula

তুমি যেকোনো project-এ এইভাবে ভাববে:

```text
ENTITY + RESPONSIBILITY
```

### Responsibility হতে পারে:

```text
Card
List
Grid
Form
Details
Profile
Summary
Filter
Search
Table
Modal
Dialog
Selector
Picker
Status
Badge
Preview
Upload
```

তাই:

```text
HotelCard
DoctorProfile
JobFilter
BookingForm
OrderSummary
PatientDetails
RoomSelector
PaymentStatus
ResumePreview
InvoiceTable
```

---

## 11. Project বড় হলে Feature-based structure রাখো

আমি তোমার React/DRF project-এর জন্য **এটাই recommend করব**:

```text
src/
│
├── components/
│   └── ui/
│       ├── Button.jsx
│       ├── Input.jsx
│       ├── Modal.jsx
│       └── Table.jsx
│
├── features/
│   │
│   ├── hotels/
│   │   ├── components/
│   │   │   ├── HotelCard.jsx
│   │   │   ├── HotelList.jsx
│   │   │   └── HotelDetails.jsx
│   │   ├── pages/
│   │   │   ├── HotelListPage.jsx
│   │   │   └── HotelDetailsPage.jsx
│   │   └── services/
│   │       └── hotelApi.js
│   │
│   ├── bookings/
│   │   ├── components/
│   │   │   ├── BookingForm.jsx
│   │   │   ├── BookingSummary.jsx
│   │   │   └── BookingStatus.jsx
│   │   ├── pages/
│   │   │   └── BookingPage.jsx
│   │   └── services/
│   │       └── bookingApi.js
│   │
│   └── payments/
│       ├── components/
│       │   ├── PaymentForm.jsx
│       │   └── PaymentStatus.jsx
│       └── services/
│           └── paymentApi.js
│
├── layouts/
│   ├── MainLayout.jsx
│   ├── AuthLayout.jsx
│   └── DashboardLayout.jsx
│
└── pages/
```

### মূল কথা

E-commerce হোক, Hospital হোক, Job Portal হোক, Logistics হোক—**naming rule বদলাবে না**।

শুধু domain entity বদলাবে:

```text
E-commerce → ProductCard
Hotel      → RoomCard
Hospital   → PatientCard
Job Portal → JobCard
Logistics  → ShipmentCard
University → StudentCard
Food       → RestaurantCard
```

অর্থাৎ **project অনুযায়ী naming convention আলাদা করার দরকার নেই; একই convention সব project-এ apply করবে।**

# folder structure rules

React project-এ folder naming-এর জন্যও একটা consistent convention রাখলে project বড় হলেও manage করা সহজ হয়।

### 1. General folder naming

আমি তোমাকে **lowercase + kebab-case** recommend করব:

```text
components/
features/
services/
hooks/
layouts/
pages/
utils/
assets/
```

একাধিক word হলে:

```text
user-profile/
booking-management/
payment-method/
product-details/
```

❌ Avoid:

```text
Components/
UserProfile/
user_profile/
UserProfileComponents/
```

---

### 2. Feature-based project হলে

তোমার Hotel / Hospital / Job Portal-এর মতো project-এ:

```text
src/
├── components/
├── features/
│   ├── hotels/
│   ├── rooms/
│   ├── bookings/
│   ├── payments/
│   └── reviews/
├── layouts/
├── pages/
├── hooks/
├── services/
├── utils/
└── assets/
```

এখানে **feature folder সাধারণত plural** রাখা convenient:

```text
hotels/
rooms/
bookings/
payments/
users/
products/
orders/
```

---

### 3. Feature-এর ভিতরে

```text
features/
└── bookings/
    ├── components/
    ├── pages/
    ├── hooks/
    ├── services/
    └── utils/
```

যেমন:

```text
features/
└── bookings/
    ├── components/
    │   ├── BookingCard.jsx
    │   ├── BookingForm.jsx
    │   └── BookingSummary.jsx
    │
    ├── pages/
    │   ├── BookingListPage.jsx
    │   └── BookingDetailsPage.jsx
    │
    ├── hooks/
    │   └── useBookings.js
    │
    └── services/
        └── bookingApi.js
```

---

### 4. `components` আর `features` কখন?

**Shared component** হলে:

```text
components/
└── ui/
    ├── Button.jsx
    ├── Input.jsx
    ├── Modal.jsx
    └── Pagination.jsx
```

শুধু Booking-এর জন্য হলে:

```text
features/
└── bookings/
    └── components/
        ├── BookingCard.jsx
        └── BookingForm.jsx
```

অর্থাৎ:

> **যেটা পুরো application-এ reusable → `components/`**
> **যেটা নির্দিষ্ট business feature-এর → `features/<feature>/`**

---

### 5. Pages-এর ক্ষেত্রে

```text
pages/
├── home/
├── login/
├── register/
├── dashboard/
└── not-found/
```

অথবা feature-based হলে page-ও feature-এর ভিতরে রাখতে পারো:

```text
features/
└── bookings/
    └── pages/
        ├── BookingListPage.jsx
        └── BookingDetailsPage.jsx
```

আমি বড় project-এ **দ্বিতীয় approach** বেশি পছন্দ করি, কারণ Booking-এর সবকিছু এক জায়গায় থাকে।

---

### 6. একটা complete example

Hotel Management:

```text
src/
│
├── components/
│   └── ui/
│       ├── Button.jsx
│       ├── Input.jsx
│       ├── Modal.jsx
│       └── Table.jsx
│
├── features/
│   ├── hotels/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   └── services/
│   │
│   ├── rooms/
│   │   ├── components/
│   │   ├── pages/
│   │   └── services/
│   │
│   ├── bookings/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   └── services/
│   │
│   └── payments/
│       ├── components/
│       ├── pages/
│       └── services/
│
├── layouts/
│   ├── MainLayout.jsx
│   ├── AuthLayout.jsx
│   └── DashboardLayout.jsx
│
├── hooks/
├── services/
├── utils/
├── lib/
├── assets/
├── routes/
└── App.jsx
```

### সহজে মনে রাখো

| Folder        | কী থাকবে                   |
| ------------- | -------------------------- |
| `components/` | Shared UI                  |
| `features/`   | Business features          |
| `pages/`      | যদি global pages থাকে      |
| `layouts/`    | Page layouts               |
| `hooks/`      | Reusable custom hooks      |
| `services/`   | API/business service       |
| `utils/`      | Helper functions           |
| `lib/`        | Library/config setup       |
| `assets/`     | Images, fonts, icons       |
| `routes/`     | React Router configuration |

**সবচেয়ে important:** folder-এর নাম lowercase রাখো, আর multi-word folder হলে `kebab-case` রাখো। Component/file-এর নাম `PascalCase` রাখো।

**kebab-case** মানে হলো একাধিক word-এর মাঝে **hyphen (`-`)** ব্যবহার করা।

### Example

```text
user-profile
product-details
booking-management
payment-method
```

এখানে:

```text
user + profile
      ↓
user-profile
```

### বিভিন্ন naming convention

| Convention     | Example            |
| -------------- | ------------------ |
| camelCase      | `userProfile`      |
| PascalCase     | `UserProfile`      |
| snake_case     | `user_profile`     |
| **kebab-case** | **`user-profile`** |
| UPPER_CASE     | `USER_PROFILE`     |

### React project-এ

**Folder:**

```text
user-profile/
product-details/
booking-management/
```

**Component:**

```text
UserProfile.jsx
ProductDetails.jsx
BookingManagement.jsx
```

অর্থাৎ সহজ rule:

> 📁 **Folder → kebab-case**
> ⚛️ **React Component → PascalCase**
> 🟨 **Variable/function → camelCase**

Example:

```text
features/
└── booking-management/
    └── components/
        └── BookingForm.jsx
```

এটাই clean এবং consistent convention।
