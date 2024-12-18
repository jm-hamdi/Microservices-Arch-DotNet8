# MicroServices

This project is a microservices-based architecture implemented using .NET 8 and Entity Framework Core. The solution consists of three micro-services: UserService, ProductService, and OrderService. MainService handle interactions between these services using Ocelot API Gateway where each is responsible for its own domain.


## Services

### MainService

- **Description**: Orchestrates operations across `UserService`, `ProductService`, and `OrderService`.
- **Endpoints**:
  - `POST GET /users/{id}` to `/api/users/{id}`
  - `POST GET /products/{id}` to `/api/products/{id}`
  - `POST GET /orders/{id}` to `/api/orders/{id}`

### UserService

- **Endpoints:**
  - `GET /api/users` - Retrieve all users.
  - `GET /api/users/{id}` - Retrieve a user by ID.
  - `POST /api/users` - Add a new user.

### ProductService

- **Endpoints:**
  - `GET /api/products` - Retrieve all products.
  - `GET /api/products/{id}` - Retrieve a product by ID.
  - `POST /api/products` - Add a new product.

### OrderService

- **Endpoints:**
  - `GET /api/orders` - Retrieve all orders.
  - `GET /api/orders/{id}` - Retrieve an order by ID.
  - `POST /api/orders` - Create a new order.
  - `GET /api/orders/details/{id}` - Retrieve order details, including user and product information.
    - **Details**: Reaches UserService and ProductService. Uses `GET /api/users/{id}` and `GET /api/products/{id}` from these services to retrieve user and product information.

## Configuration

Each service has its own database context and is configured to use Entity Framework Core for data access. The services are set up to communicate with each other through HTTP requests.

### MainService

- **Port:** 7133
- **DTOs:** `UserDto`, `ProductDto`, `OrderDto`
- **Dependencies:** Requires `UserService`, `ProductService` and `OrderService` to be running.
  - **Note**: `MainService` simplifies the interaction with the microservices by providing a unified interface.

### UserService

- **Port:** 7188
- **Database Context:** `UserContext`
- **Models:** `User`

### ProductService

- **Port:** 7197
- **Database Context:** `ProductContext`
- **Models:** `Product`

### OrderService

- **Port:** 7138
- **Database Context:** `OrderContext`
- **Models:** `Order`

## Swagger

Each service includes Swagger for testing. You can access these at the following URLs:

- UserService: `https://localhost:7188/swagger`
- ProductService: `https://localhost:7197/swagger`
- OrderService: `https://localhost:7138/swagger`

## Postman

Each service is accessible from MainService. You can access these by making `GET` or `POST` request in Postman:

- UserService: `https://localhost:7133/users/`
- ProductService: `https://localhost:7133/products/`
- OrderService: `https://localhost:7133/orders/`
