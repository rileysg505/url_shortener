

### Assignment: URL Shortening Service Using Go and Microservices

#### Objective
Build a URL Shortening Service using Go with a microservice architecture. This service will allow users to shorten URLs, redirect to the original URLs, and track usage analytics.

#### Requirements
- **Programming Language**: Go
- **Database**: Your choice (e.g., PostgreSQL, MongoDB, or Redis)
- **Microservices**: Each core function (URL shortening, redirection, analytics) should be its own microservice.
- **API Gateway (Optional)**: You can add an API Gateway if you’d like to route traffic through a unified entry point.

### Key Functional Requirements

1. **URL Shortening**: Create a service where users can submit a long URL and receive a shortened URL in return. Implement the logic to create short URL codes and ensure these codes are unique.
   
2. **Redirection**: Create a service responsible for handling the redirection when a short URL is accessed. It should decode the shortened URL, retrieve the original URL from storage, and redirect the user accordingly.

3. **Analytics (Optional)**: Implement a service that logs and tracks data such as the number of times a short URL has been accessed, timestamps, and user information (e.g., IP address or country, if available).

4. **Scalability**: Use a microservice architecture so that each service can be scaled independently.

### Project Structure (Suggested)

Organize your codebase as follows:

```
url_shortener_project/
│
├── services/
│   ├── url_shortener/
│   │   ├── cmd/
│   │   │   └── main.go              # Entry point for the URL shortener service
│   │   ├── internal/
│   │   │   ├── handler/             # HTTP handlers
│   │   │   ├── storage/             # Database or storage logic
│   │   │   ├── models/              # Data models (e.g., URL struct)
│   │   │   └── config/              # Configuration setup
│   │   ├── Dockerfile
│   │   ├── go.mod
│   │   └── go.sum
│   │
│   ├── redirection/
│   └── analytics/
│
├── api_gateway/                     # API Gateway (if implemented)
├── config/                           # Central config files
├── scripts/                          # Scripts for automation
├── docker-compose.yml
└── README.md
```

### Assignment Guidelines

#### Part 1: Set Up Go Modules and Folder Structure
1. **Go Modules**: Initialize Go modules for each microservice. Run `go mod init` within each service directory to manage dependencies independently.
2. **Folder Structure**: Follow the recommended structure, ensuring each microservice has its own `cmd/` for the main entry point and `internal/` for service-specific packages.

#### Part 2: Implement the URL Shortening Service
1. **Generate Short URLs**: Implement an algorithm to create a unique short code for each long URL.
2. **Storage**: Decide on a storage solution (e.g., Redis for in-memory storage or PostgreSQL for persistence).
3. **HTTP Handlers**: Implement HTTP endpoints in `handler/` for creating short URLs.
4. **Configuration**: Use environment variables for configuration. You can store environment-specific settings in `config/`.

#### Part 3: Implement the Redirection Service
1. **Decoding Short URLs**: Implement logic in `handler/` that decodes a short URL and fetches the original URL from storage.
2. **Redirection Logic**: Set up the HTTP handler to redirect users to the original URL.
3. **Error Handling**: Ensure proper error handling for cases where a short URL is not found.

#### Part 4: Implement Optional Analytics Service
1. **Tracking Data**: Track data for each URL access, such as request timestamps and user details (if available).
2. **Data Storage**: Store analytics data in a separate storage solution if necessary, or add tables to your existing database.
3. **API Endpoints**: Create HTTP endpoints to retrieve analytics data.

#### Part 5: Containerization with Docker
1. **Dockerize Each Service**: Write a Dockerfile for each service to containerize your Go application.
2. **Docker Compose**: Create a `docker-compose.yml` to orchestrate multiple services, including any database containers.
   
#### Part 6: Testing and Documentation
1. **Unit Tests**: Write unit tests for core functions within each service. Use Go’s built-in testing tools (`_test.go` files).
2. **Documentation**: Write a `README.md` explaining your services, how to set up the environment, and instructions for running the application.

#### Part 7: API Gateway (Optional)
If you choose to implement an API Gateway:
1. **Routing**: Configure the API Gateway to route incoming requests to the appropriate service.
2. **Security and Throttling**: Optionally, add basic rate limiting or request validation at the gateway level.

### Bonus Challenges
- **Concurrency**: Use Go’s goroutines to handle concurrent requests efficiently.
- **Rate Limiting**: Implement a basic rate-limiting mechanism to limit the number of requests a user can make to the URL shortening service.
- **CI/CD**: Set up a CI/CD pipeline to automatically build and deploy your containers on each commit.

### Submission Requirements
Submit your code in a GitHub repository with the following:
- Code for each service following the specified structure.
- A `requirements.txt` or `go.mod` file for each service.
- Dockerfile for each service and a `docker-compose.yml` for orchestration.
- Instructions in `README.md` on how to set up and run the project.

### Evaluation Criteria
- **Code Quality**: Clear and organized code, with logical function separation.
- **Functionality**: Each service fulfills its role accurately (shortening, redirection, analytics).
- **Testing**: Adequate test coverage for core functions.
- **Documentation**: Clear instructions for setting up and using the application.
- **Bonus**: Implementation of optional features, such as the API Gateway or concurrency handling.

