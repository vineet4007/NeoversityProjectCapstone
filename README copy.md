# Neoversity Project - Microservices Architecture

## Project Overview
This is a comprehensive microservices-based e-commerce platform developed as part of the Master of Science in Computer Science degree project. The project demonstrates modern software architecture patterns including microservices, service discovery, API gateway, and distributed systems.

## Architecture Overview

### Microservices Architecture
The project follows a microservices architecture pattern with the following services:

1. **API Gateway** (`apigateway-service`) - Port 6000
   - Entry point for all client requests
   - Route management and load balancing
   - Service discovery integration

2. **Service Discovery** (`service-discovery`) - Port 8761
   - Eureka server for service registration and discovery
   - Central registry for all microservices

3. **User Authentication Service** (`user-auth-service`) - Port 9090
   - User registration and authentication
   - JWT token management
   - User role management

4. **Product Service** (`product-service`) - Port 8080
   - Product catalog management
   - Category management
   - Product search and filtering

5. **Payment Service** (`payment-service`) - Port 9091
   - Payment processing
   - Transaction management

6. **Email Service** (`email-service`) - Port (dynamic)
   - Email notifications
   - Communication service

## Technology Stack

### Backend
- **Framework**: Spring Boot 3.5.x
- **Language**: Java 17
- **Build Tool**: Maven
- **Database**: MySQL
- **Cache**: Redis
- **Service Discovery**: Netflix Eureka
- **API Gateway**: Spring Cloud Gateway
- **Load Balancer**: Spring Cloud LoadBalancer

### Development Tools
- **Lombok**: For reducing boilerplate code
- **Spring DevTools**: For development convenience
- **Docker**: For containerization

## Project Structure

```
NeoversityProject/
├── apigateway-service/         # API Gateway Service
├── service-discovery/          # Eureka Service Discovery
├── user-auth-service/          # Authentication Service
├── product-service/            # Product Management Service
├── payment-service/            # Payment Processing Service
└── email-service/              # Email Notification Service
```

## Service Details

### API Gateway (Port 6000)
- **Purpose**: Central entry point for all client requests
- **Features**: 
  - Route configuration for different services
  - Load balancing using Spring Cloud LoadBalancer
  - Service discovery integration with Eureka
- **Routes**:
  - `/products/*` → Product Service
  - `/users/*` → User Service (commented)

### Service Discovery (Port 8761)
- **Purpose**: Service registry and discovery
- **Technology**: Netflix Eureka Server
- **Features**: Service registration, health monitoring, service discovery

### User Authentication Service
- **Database**: MySQL (authservice_june)
- **Features**:
  - User registration and login
  - JWT token generation
  - Role-based access control
  - User management
- **Endpoints**:
  - `POST /auth/signup` - User registration
  - `POST /auth/login` - User authentication

### Product Service
- **Database**: MySQL (productservicemay25)
- **Cache**: Redis (localhost:6379)
- **Features**:
  - Product CRUD operations
  - Category management
  - Product search and filtering
  - Pagination support
- **Endpoints**:
  - `GET /products/{id}` - Get single product
  - `GET /products/` - Get all products
  - `POST /products` - Create product
  - `GET /products/title/{title}/{pageNumber}/{pageSize}` - Search by title with pagination

## Database Schema

### Product Service Database
- **Products Table**: id, title, price, description, imgUrl, category_id
- **Categories Table**: id, name
- **Base Model**: id, createdAt, updatedAt

### User Service Database
- **Users Table**: id, name, email, password, phoneNumber
- **Roles Table**: id, name
- **User_Roles Table**: user_id, role_id (Many-to-Many relationship)

## Configuration

### Environment Variables
- `PRODUCT_SERVICE_PORT_NUMBER` - Product service port
- `DB_URL` - Database connection URL
- `DB_USERNAME` - Database username
- `DB_PASSWORD` - Database password

### Database Configuration
- **Product Service**: MySQL on localhost:3306
- **User Service**: MySQL on localhost:3306
- **Redis**: localhost:6379

## Running the Project

### Prerequisites
1. Java 17 or higher
2. Maven 3.6+
3. MySQL 8.0+
4. Redis (for caching)
5. Docker (optional)

### Setup Instructions

1. **Start Service Discovery**:
   ```bash
   cd service-discovery
   mvn spring-boot:run
   ```

2. **Start User Authentication Service**:
   ```bash
   cd user-auth-service
   mvn spring-boot:run
   ```

3. **Start Product Service**:
   ```bash
   cd product-service
   mvn spring-boot:run
   ```

4. **Start API Gateway**:
   ```bash
   cd apigateway-service
   mvn spring-boot:run
   ```

5. **Start Other Services** (Payment, Email):
   ```bash
   cd payment-service
   mvn spring-boot:run
   
   cd email-service
   mvn spring-boot:run
   ```

### Docker Deployment
```bash
# Build and run Product Service
cd product-service
mvn clean package
docker build -t product-service .
docker run -p 8080:8080 product-service
```

## API Endpoints

### Product Service (via API Gateway)
- `GET http://localhost:6000/api/products/{id}` - Get product by ID
- `GET http://localhost:6000/api/products/` - Get all products
- `POST http://localhost:6000/api/products` - Create new product

### User Service
- `POST http://localhost:9090/auth/signup` - User registration
- `POST http://localhost:9090/auth/login` - User login

## Monitoring and Health Checks

### Eureka Dashboard
- **URL**: http://localhost:8761
- **Purpose**: View registered services and their health status

### Service Health Endpoints
- Each service provides health check endpoints
- Monitor service status and dependencies

## Development Features

### Code Quality
- **Lombok**: Reduces boilerplate code
- **Spring Boot DevTools**: Hot reload and development convenience
- **Exception Handling**: Centralized exception handling
- **Validation**: Input validation using Spring Validation

### Testing
- **JUnit 5**: Unit testing framework
- **Spring Boot Test**: Integration testing
- **Test Coverage**: Comprehensive test coverage

## Future Enhancements

1. **Security**: Implement OAuth2 and JWT token validation
2. **Monitoring**: Add Prometheus and Grafana for metrics
3. **Logging**: Centralized logging with ELK stack
4. **CI/CD**: Automated deployment pipeline
5. **API Documentation**: Swagger/OpenAPI documentation
6. **Rate Limiting**: Implement API rate limiting
7. **Circuit Breaker**: Add resilience patterns

## Author
**Vineet Kumar**  
Master of Science in Computer Science  
Email: vineet4007@gmail.com

## Version
1.0.0

## License
This project is developed for academic purposes as part of the Master's degree program.
