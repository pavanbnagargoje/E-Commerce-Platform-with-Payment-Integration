# NexaCart: Modern E-Commerce Platform

A production-ready, full-stack **E-Commerce Platform** built using **.NET 8/9, Blazor, and ASP.NET Core Web API**. The project showcases enterprise design patterns, high-performance distributed caching, secure third-party checkout flows, and automated deployment pipelines.

## Key Features

- **Authentication & Security:** Secure user identity management leveraging ASP.NET Core Identity and JWT tokens.
- **Distributed Caching:** Lightning-fast shopping cart persistence and session state managed via Redis.
- **Payment Integration:** Secure checkout flows powered by the Stripe API with webhook handling for order processing.
- **Database & ORM:** Code-first database management using Entity Framework Core and SQL Server.
- **Modern UI:** Responsive, real-time administrative dashboards and customer storefronts built with Blazor Server and Tailwind CSS.
- **Observability:** Centralized structured logging utilizing Serilog.

---

## Architecture & Tech Stack

The application follows the principles of **Clean Architecture**, separating concerns into isolated layers to maximize testability and maintainability.

- **Frontend:** Blazor Server, Tailwind CSS, SignalR
- **Backend API:** ASP.NET Core Web API, Minimal APIs
- **Database:** Microsoft SQL Server
- **Caching:** Redis (Distributed Caching)
- **ORM:** Entity Framework Core
- **Payments:** Stripe .NET SDK

---

## Getting Started

### Prerequisites

Ensure you have the following installed locally:

- [.NET SDK 8.0 / 9.0](https://microsoft.com)
- [Docker Desktop](https://docker.com) (for running SQL Server and Redis infrastructure)
- [Stripe CLI](https://stripe.com) (for testing local payment webhooks)

### Installation & Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com
   cd nexacart-ecommerce
   ```

2. **Spin up local infrastructure:**
   Run the pre-configured Docker Compose file to start SQL Server and Redis instances:

   ```bash
   docker-compose up -d
   ```

3. **Configure Environment Variables:**
   Navigate to the API project directory and create/update your `appsettings.Development.json`:

   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Server=localhost,1433;Database=NexaCartDb;User Id=sa;Password=YourSecurePassword123!;TrustServerCertificate=True;"
     },
     "Redis": {
       "Configuration": "localhost:6379"
     },
     "Stripe": {
       "SecretKey": "sk_test_...",
       "PublishableKey": "pk_test_...",
       "WebhookSecret": "whsec_..."
     }
   }
   ```

4. **Run Database Migrations:**

   ```bash
   dotnet ef database update --project src/NexaCart.Infrastructure --startup-project src/NexaCart.API
   ```

5. **Start the Application:**
   ```bash
   dotnet run --project src/NexaCart.API
   ```

---

## 🧪 Testing

The solution includes a comprehensive test suite covering business logic, domain constraints, and API routing.

- **Unit Tests:** Handled via `xUnit` and `Moq`.
- **Integration Tests:** Built using `Microsoft.AspNetCore.Mvc.Testing` and `Testcontainers` to spin up disposable databases dynamically.

To execute the test suite, run:

```bash
dotnet test
```
