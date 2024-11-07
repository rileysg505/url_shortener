### Assignment: Build a URL Shortening Microservices Application

#### Overview
Your task is to develop a URL shortening application using a microservices architecture. Each service will be responsible for a specific functionality, making the application more modular, scalable, and resilient.

#### Project Objectives
- **Implement a REST API** that accepts a long URL, generates a shortened URL, and redirects users from the short URL to the original URL.
- **Design a microservices architecture** where each core feature (URL shortening, redirection, analytics, etc.) is encapsulated in a separate service.
- **Utilize a database** to store URL mappings and manage them efficiently.
- **Ensure scalability** by designing with potential traffic and data growth in mind.

#### Functional Requirements
1. **Shorten URL Service**: Accepts a long URL and returns a short URL. The response should include a unique identifier.
2. **Redirection Service**: Redirects users from a short URL to the original long URL.
3. **Key Generation Service** (Optional): A service that generates unique identifiers for URLs to keep the shortening logic separate and scalable.
4. **Analytics Service** (Optional): Tracks and retrieves data on URL usage (e.g., visit count, last accessed time).

#### Technical Requirements
- **Language and Framework**: Use Python (with Flask, FastAPI, or Django) or another language/framework you prefer.
- **Database**: Choose an appropriate database (e.g., PostgreSQL, MySQL, Redis) and ensure it’s accessible to relevant services.
- **Service Communication**: Use HTTP or gRPC for communication between services.
- **Configuration**: Store sensitive data (e.g., database credentials) securely, using environment variables.

#### Microservices Design Guidelines

##### Part 1: Service Planning and Architecture
- **Define Service Responsibilities**: Determine the core services needed for the application (URL Shortener, Key Generation, Redirection, Analytics). Decide on the boundaries and responsibilities for each service.
- **Service Communication**: Decide how services will communicate. For example, the URL Shortener might call the Key Generation Service over HTTP to get a unique ID.
- **Data Storage and Sharing**: Each service should handle its own data storage, but they can share a centralized database for storing URLs or use separate databases as needed.

##### Part 2: Core Services Implementation
1. **URL Shortener Service**:
   - Handles incoming requests to shorten URLs, delegates key generation to the Key Generation Service if implemented, and stores the mappings.
   - Exposes a `POST /shorten` endpoint for URL shortening.
   
2. **Key Generation Service** (Optional):
   - Responsible for generating unique identifiers for shortened URLs. Choose a method that avoids collision and can handle high volumes of requests.
   - Exposes a `GET /generate-key` endpoint to return a new key.

3. **Redirection Service**:
   - Handles requests to redirect users from the short URL to the original URL.
   - Exposes a `GET /<short_url_id>` endpoint, retrieves the original URL, and performs a 302 redirect.
   
4. **Analytics Service** (Optional):
   - Tracks data like click counts and last access time for each URL. This can be as simple as incrementing a counter in a database.
   - Exposes an endpoint like `GET /analytics/<short_url_id>` to retrieve analytics.

##### Part 3: Deployment and Orchestration
- **Docker**: Containerize each service with Docker to make it easy to deploy and scale each service independently.
- **Orchestration**: Use Docker Compose for local development or Kubernetes for cloud-based deployment. Each service should run in its own container.
- **Reverse Proxy**: Use an NGINX or API gateway to route external requests to the appropriate service.

##### Part 4: Testing and Monitoring
- **Unit and Integration Tests**: Ensure each service has independent unit and integration tests. For instance, the URL Shortener Service should be tested for its ability to create new shortened URLs.
- **Service Health Monitoring**: Use monitoring tools (e.g., Prometheus, Grafana) to track each service’s performance and health, especially for response times and error rates.

#### Evaluation Criteria
- **Functionality**: Each service works independently and integrates correctly within the application.
- **Microservices Design**: The application is modular, with clear service boundaries and communication patterns.
- **Scalability**: Services are stateless, or state is managed effectively, allowing easy horizontal scaling.
- **Testing and Monitoring**: Adequate tests are implemented, and monitoring is configured for service health and metrics tracking.

#### Bonus Points
- **Implementing a CI/CD Pipeline**: Set up an automated pipeline for testing and deploying services.
- **Using gRPC for Service Communication**: This can improve performance and type safety between services.
- **Advanced Analytics**: Add features like geographic tracking or device usage stats in the Analytics Service.

