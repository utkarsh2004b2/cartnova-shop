# 🛒 CartNova – Full-Stack E-Commerce Web Application
### Built with Java, Spring Boot, Google OAuth2, Thymeleaf & MySQL

CartNova is a full-featured **e-commerce web application** with a modern UI, a complete shopping flow, admin product management, secure Google OAuth login, order history with PDF invoices, and a layered backend architecture.
The app is deployed on Render (Docker) and uses MySQL hosted on Aiven.

---

## 🚀 Live Demo
🔗 **https://cartnova-ookc.onrender.com**

> Note: The app runs on free-tier hosting, so the first load after inactivity can take 30–50 seconds. Google login works only for approved test users while the OAuth app is in testing mode.

---

## 📌 Overview
CartNova provides a shopping experience similar to a real e-commerce platform, including:

- Product browsing and search
- Add to cart
- Checkout summary
- Razorpay payment integration (disabled in the live demo)
- Order tracking
- Invoice downloads
- Admin product management
- Google OAuth authentication
- Responsive UI

---

## 🎯 Key Features

### 👤 User Features
- Login using **Google OAuth 2.0**
- View all products with clean product cards
- Product details page
- Add to cart with live cart count update
- Checkout page showing:
  - Product price
  - Delivery charge
  - Discounts
  - Payable total
- **Razorpay payment integration** (test mode; needs API keys, not enabled in the live demo)
- Order creation on successful payment
- Payment success and failure redirection
- View previous orders under **My Orders**
- **Order Details** page showing order ID, product details, amount, timestamps and payment status
- **Download invoice (PDF)** for each order

### 🛠️ Admin Features
Admin users are identified by email addresses configured in the `ADMIN_EMAILS` environment variable.

- Google OAuth2 login with admin role
- Add product (with server-side validations)
- Edit product (form pre-filled with current values)
- Delete product
- Product image upload:
  - JPG / PNG only
  - Max 1 MB
  - Stored in the database
- Admin UI hides the Add to Cart and Buy buttons

⚠ **Admin accounts cannot order or add to cart.**

---

## 💳 Payment Integration (Razorpay)
- Razorpay checkout integrated using the Razorpay Java SDK
- Backend verifies the payment signature
- **Success flow:** save order to the database, clear the cart, redirect to the success page
- **Failure flow:** keep the cart unchanged, redirect to the failure page
- Requires `RAZORPAY_KEY` and `RAZORPAY_SECRET` (test keys). These are not configured in the live demo.

---

## 📄 Invoice Generation
Each successful order generates a **PDF invoice** with:

- Order ID
- Product details
- Payment status
- Total amount
- Order timestamp

---

## 🔧 Technologies Used

### Backend
- **Java 21**
- Spring Boot 3
- Spring MVC
- Spring Security (OAuth2 Login)
- Spring Data JPA
- Hibernate
- Maven
- Razorpay Java SDK

### Frontend
- HTML5
- CSS3
- JavaScript
- Thymeleaf
- Bootstrap

### Database
- MySQL (hosted on Aiven Cloud)

### Deployment
- Docker
- Render (Web Service)

---

## ⚙️ Configuration
Secrets are not stored in the code. Set these environment variables before running:

| Variable | Description |
|---|---|
| `DB_URL` | JDBC URL, e.g. `jdbc:mysql://localhost:3306/cartnova` |
| `DB_USERNAME` | Database username |
| `DB_PASSWORD` | Database password |
| `GOOGLE_CLIENT_ID` | Google OAuth client ID |
| `GOOGLE_CLIENT_SECRET` | Google OAuth client secret |
| `ADMIN_EMAILS` | Comma-separated admin email addresses |
| `RAZORPAY_KEY` | Razorpay key ID (optional) |
| `RAZORPAY_SECRET` | Razorpay key secret (optional) |

---

## ▶️ Run Locally
1. Install **Java 21** and **MySQL**, then create a database.
2. Create a Google OAuth client and add `http://localhost:8080/login/oauth2/code/google` as a redirect URI.
3. Set the environment variables from the table above.
4. Start the app:
```bash
   ./mvnw spring-boot:run
```
5. Open
