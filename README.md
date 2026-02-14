# Micro Electronics E-Commerce Backend API

## Setup Instructions

1. Make sure MongoDB is running on your local machine
2. Install dependencies: `npm install`
3. Start the server: `npm start`
4. Server will run on: `http://localhost:3000`

## API Endpoints

### Authentication

#### Register User
- **POST** `/api/auth/register`
- Body:
```json
{
  "email": "user@example.com",
  "password": "password123",
  "role": "user"
}
```
- For admin: use `"role": "admin"`

#### Login
- **POST** `/api/auth/login`
- Body:
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```
- Returns: `token` (use this in Authorization header for protected routes)

---

### Products

**Note:** All product routes require authentication. Add header: `Authorization: Bearer YOUR_TOKEN`

#### Get All Products
- **GET** `/api/products`

#### Search Products
- **GET** `/api/products/search?name=laptop`

#### Get Single Product
- **GET** `/api/products/:id`

#### Create Product (Admin Only)
- **POST** `/api/products`
- Body:
```json
{
  "name": "Laptop",
  "price": 999.99,
  "stock": 50,
  "description": "High-performance laptop"
}
```

#### Update Product (Admin Only)
- **PUT** `/api/products/:id`
- Body:
```json
{
  "name": "Updated Laptop",
  "price": 899.99,
  "stock": 45
}
```

#### Delete Product (Admin Only)
- **DELETE** `/api/products/:id`

---

### Shopping Cart

**Note:** All cart routes require authentication.

#### Get Cart
- **GET** `/api/cart`

#### Add Item to Cart
- **POST** `/api/cart/add`
- Body:
```json
{
  "productId": "PRODUCT_ID_HERE",
  "quantity": 2
}
```

#### Update Cart Item
- **PUT** `/api/cart/update/:productId`
- Body:
```json
{
  "quantity": 3
}
```

#### Remove Item from Cart
- **DELETE** `/api/cart/remove/:productId`

---

### Orders

**Note:** All order routes require authentication.

#### Checkout (Create Order)
- **POST** `/api/orders/checkout`
- Creates order from current cart and clears the cart

#### Get My Orders
- **GET** `/api/orders/my-orders`

#### Get Single Order
- **GET** `/api/orders/:id`

---

## Testing Flow with Postman

1. **Register an admin user** (role: "admin")
2. **Register a regular user** (role: "user")
3. **Login as admin** → save the token
4. **Create products** using admin token
5. **Login as regular user** → save the token
6. **Browse products** using user token
7. **Add products to cart**
8. **View cart and total**
9. **Update quantities or remove items**
10. **Checkout** to create order
11. **View orders**

## Key Features

✅ Secure password hashing with bcrypt
✅ JWT authentication
✅ Role-based access (user/admin)
✅ Stock validation (prevents ordering more than available)
✅ Cart management (add, update, remove)
✅ Order creation with automatic stock reduction
✅ Cart clearing after checkout
✅ Product search functionality

## Notes

- Cart is automatically created for users when they first add an item
- After checkout, the cart becomes inactive and a new cart is created for next purchase
- Stock is automatically reduced when order is placed
- Admin can manage all products
- Users can only view products and manage their own cart/orders
