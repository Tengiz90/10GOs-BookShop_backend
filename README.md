# 📚 10GO's Books .NET 10 API

Backend API documentation for the **10GO's Books** project built with .NET 10.

- **Base URL:** `https://tg-books-backend-gyfhgbaye3evbpek.polandcentral-01.azurewebsites.net`
- **Authentication:** Upon successful login (`POST /api/users/sign-in`), a JWT Bearer token containing the authenticated account's assigned role (`Customer` or `Admin`) is generated for the session.
- **Email Verification:** Upon registering a new account (`POST /api/users/register`), a 4-digit verification code is emailed to the user. Note that to confirm the email via `POST /api/users/confirm-email`, the user must be authenticated (an active JWT Bearer token must be included in the request header).

---

## API Endpoints

### Authors
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/authors/get-all` | Retrieve all authors |

---

### Books
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/books/get-by-category` | Fetch books filtered by category |
| `GET` | `/api/books/{id}` | Fetch detailed information for a specific book by ID |
| `GET` | `/api/books/page` | Fetch a paginated list of books |
| `GET` | `/api/books/get-by-on-sale` | Fetch books currently on sale |
| `PUT` | `/api/books/edit` | Update existing book details (Admin access) |
| `POST` | `/api/books/add` | Add a new book (Admin access) |
| `GET` | `/api/books/get-by-author` | Fetch books by a specific author |
| `DELETE` | `/api/books/delete` | Soft-delete a book (Admin access) |
| `GET` | `/api/books/get-deleted` | Fetch all soft-deleted books (Admin access) |
| `PUT` | `/api/books/undelete` | Restore a previously deleted book (Admin access) |

#### Book Search & Pagination (`GET /api/books/page`)

The `/api/books/page` endpoint allows querying the book catalog using dynamic query parameters for filtering alongside standard pagination parameters.

**Available Query Parameters**

* **`title`** (`string`, optional): Case-insensitive keyword filter matching book titles.
* **`categoryId`** (`integer`, optional): Numeric ID used to filter books belonging to a specific category.
* **`onSale`** (`boolean`, optional): Boolean flag to filter books by sale status (`true` / `false`).
* **`pageNumber`** (`integer`, default: `1`): The target page index to retrieve.
* **`pageSize`** (`integer`, default: `20`): Total number of book records returned per page response.

---

### Categories
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/categories/get-all` | Retrieve all available book categories |
| `GET` | `/api/categories/get-name/{id}` | Retrieve category name by ID |

---

### Orders
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/orders/get-all` | Retrieve all orders (Admin access) |
| `GET` | `/api/orders/get-by-user` | Retrieve order history for the authenticated user |

---

### Users
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/users/buy-books` | Process a purchase for items in the user's cart |
| `POST` | `/api/users/register` | Register a new user account and dispatch a 4-digit confirmation code via email |
| `POST` | `/api/users/confirm-email` | Confirm a newly registered user's email address using the received 4-digit code (Requires JWT Bearer token) |
| `POST` | `/api/users/sign-in` | Authenticate user/admin and issue a new JWT token containing role claims (`Customer` or `Admin`) |
| `GET` | `/api/users/billing-info` | Fetch billing information for the user |
| `PUT` | `/api/users/edit-name` | Update user's profile name |
| `PUT` | `/api/users/edit-billing-address` | Update user's billing address |
| `GET` | `/api/users/cart` | Retrieve user's current shopping cart contents |
| `POST` | `/api/users/cart` | Add an item to the shopping cart |
| `DELETE` | `/api/users/cart` | Remove an item from the shopping cart |
| `PUT` | `/api/users/cart` | Update item quantities or state in the cart |

---

### Analytics
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/analytics/export-books-ml-data` | Export books data for ML model training |
| `GET` | `/api/analytics/export-author-ml-data` | Export author data for ML model training |
| `GET` | `/api/analytics/export-click-ml-data` | Export user click/interaction data for ML training |

---

## Used Libraries & Dependencies

| Library | Version | Description |
| :--- | :--- | :--- |
| **Azure.Storage.Blobs** | `12.27.0` | Azure Blob Storage integration for handling binary and text file uploads. |
| **BCrypt.Net-Next** | `4.1.0` | Secure password hashing using the BCrypt algorithm. |
| **FluentValidation** | `10.4.0` | Strongly-typed validation rules engine for building clean request models. |
| **FluentValidation.DependencyInjectionExtensions** | `10.4.0` | Dependency Injection support for registering FluentValidation validators. |
| **Microsoft.AspNetCore.Authentication.JwtBearer** | `10.0.3` | Middleware enabling JWT Bearer token authentication in ASP.NET Core. |
| **Microsoft.AspNetCore.OpenApi** | `10.0.3` | OpenAPI endpoint annotations and route handling utilities. |
| **Microsoft.EntityFrameworkCore** | `10.0.3` | Object-Relational Mapper (ORM) for data management, change tracking, and queries. |
| **Microsoft.EntityFrameworkCore.Design** | `10.0.3` | Shared design-time components for Entity Framework Core tooling. |
| **Microsoft.EntityFrameworkCore.SqlServer** | `10.0.3` | Microsoft SQL Server database provider for Entity Framework Core. |
| **Microsoft.EntityFrameworkCore.Tools** | `10.0.3` | Package Manager Console tools for executing database migrations and scaffolding. |
| **Swashbuckle.AspNetCore** | `10.1.4` | Swagger tooling for API interactive UI and OpenAPI spec generation. |
