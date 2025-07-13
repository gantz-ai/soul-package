# Jet Framework 🚀

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/soul-lang/soul-package)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Soul](https://img.shields.io/badge/soul-compatible-purple.svg)](https://soul-lang.org)

A modern, powerful, and enterprise-grade web framework for the Soul programming language. Jet combines the simplicity of Express.js with the robustness of enterprise frameworks, built specifically for Soul with advanced features like built-in authentication, validation, database integration, real-time capabilities, and comprehensive security measures.

## 🌟 Why Choose Jet?

- **🔥 Performance First** - Built on Soul's high-performance runtime with zero-copy optimizations
- **🛡️ Security by Default** - Enterprise-grade security features built-in, not bolted-on
- **🔧 Developer Experience** - Intuitive API with excellent TypeScript-like type safety
- **🚀 Production Ready** - Battle-tested features for scalable applications
- **🔌 Extensible** - Rich plugin ecosystem and flexible architecture
- **📚 Well Documented** - Comprehensive documentation with real-world examples

## 🚀 Features

### Core Web Server
- **HTTP Server** - Built on Soul's HTTP module with configurable port and settings
- **Routing System** - HTTP method routing (GET, POST, PUT, DELETE, etc.) with path parameters
- **Middleware Pipeline** - Composable middleware system with request/response processing
- **Static File Serving** - Built-in static file handler with MIME type detection and security
- **Template Engine** - HTML rendering with variable interpolation, layouts, and helpers
- **Error Handling** - Global error handlers with custom error pages

### Built-in Middleware
- **CORS Support** - Cross-Origin Resource Sharing with configurable origins and headers
- **Security Headers** - Helmet-style security middleware (XSS, frame options, CSP)
- **Rate Limiting** - Request rate limiting with configurable windows and thresholds
- **Compression** - Response compression middleware
- **Request Logging** - Built-in request/response logging

### Architecture Components
- **Route Groups** - Organize routes with prefixes and shared middleware
- **Fluent API** - Method chaining for route configuration
- **Controller Integration** - MVC pattern support with controller registration
- **Service Layer** - Service and repository pattern support
- **Performance Tracking** - Basic performance metrics and health checks

### Plugin System
- **Authentication Plugin** - JWT, session, and API key authentication strategies
- **Database Plugin** - Database integration and ORM-like features
- **Validation Plugin** - Request validation with custom rules
- **Extensible Architecture** - Plugin system for adding custom functionality

## 📦 Installation

### Prerequisites

- Soul Programming Language (v2.0.0 or higher)
- Operating System: Linux, macOS, or Windows
- Memory: Minimum 512MB RAM, Recommended 2GB+
- Network: Internet connection for initial setup

### Installation Methods

#### Method 1: Soul Package Manager (Recommended)

```bash
# Install via Soul package manager
soul install jet@1.0.0

# Create new Jet project
soul create my-jet-app --template=jet
cd my-jet-app
```

#### Method 2: Git Clone

```bash
# Clone the Soul framework repository
git clone https://github.com/soul-lang/soul-package.git
cd soul-package/framework/jet

# Copy to your project
cp -r . /path/to/your/project/
```

#### Method 3: Direct Import

```soul
// In your Soul project file
import { createJet } from "soul-package/framework/jet.soul"

// Or import specific modules
import { 
    createJet, 
    Router, 
    Middleware, 
    Plugin 
} from "soul-package/framework/jet.soul"
```

### Project Initialization

```bash
# Initialize new Jet project with starter template
soul init jet-app
cd jet-app

# Install dependencies
soul deps install

# Start development server
soul dev
```

### Verification

```soul
// test-installation.soul
import { createJet } from "soul-package/framework/jet.soul"

app = createJet(3000)

app.get("/health", soul(req, res) {
    res.json({ 
        status: "ok", 
        framework: "Jet",
        version: "1.0.0",
        timestamp: Date.now()
    })
})

app.listen(soul() {
    Console.log("✅ Jet framework installed successfully!")
    Console.log("🌐 Visit: http://localhost:3000/health")
})
```

### Environment Setup

```bash
# Create environment configuration
echo "PORT=3000
NODE_ENV=development
JWT_SECRET=your-secret-key
DB_URL=postgres://localhost:5432/jetapp" > .env

# Create basic project structure
mkdir -p {routes,middleware,models,config,public,tests}
```

## 🏃‍♂️ Quick Start

### 🚀 Basic Server (30 seconds)

```soul
import { createJet } from "soul-package/framework/jet.soul"

// Create app instance with port
app = createJet(3000)

// Configure environment
app.env("development")
app.set("trustProxy", false)

// Basic route with response helpers
app.get("/", soul(req, res) {
    res.json({ 
        message: "Hello from Jet!",
        timestamp: time.now(),
        version: "1.0.0"
    })
})

// RESTful API endpoints
app.get("/api/status", soul(req, res) {
    res.status(200).json({ 
        status: "healthy", 
        uptime: time.now() - app.startTime,
        version: "1.0.0"
    })
})

app.post("/api/echo", soul(req, res) {
    res.json({ echo: req.body, headers: req.headers })
})

// Health check endpoint
app.get("/health", soul(req, res) {
    res.json(app.health())
})

// Start server
app.listen(soul() {
    Console.log("🚀 Jet server running on port 3000")
    Console.log("🌐 Visit: http://localhost:3000")
    Console.log("🏥 Health check: http://localhost:3000/health")
})
```

### ⚡ Production-Ready Server (2 minutes)

```soul
import { createJet } from "soul-package/framework/jet.soul"

// Create production-configured app
app = createJet(8080)
app.env("production")
app.set("trustProxy", true)

// Security middleware stack
app.use(app.helmet({ contentSecurityPolicy: true, frameguard: true }))
app.use(app.cors({ 
    origin: ["https://example.com", "https://app.example.com"],
    methods: ["GET", "POST", "PUT", "DELETE"],
    credentials: true
}))
app.use(app.rateLimit({ windowMs: 15 * 60 * 1000, max: 100 }))
app.use(app.compression({ level: 6, threshold: 1024 }))

// Request logging middleware
app.use(soul(req, res, next) {
    startTime = time.now()
    app.logger.info("Request: " + req.method + " " + req.path)
    
    // Override res.end to log completion
    originalEnd = res.end
    res.end = soul(data) {
        duration = time.now() - startTime
        app.logger.info("Response: " + res.statusCode + " in " + duration + "ms")
        originalEnd.call(res, data)
    }
    
    next()
})

// Static file serving
app.use("/static", app.static("/static", "./public"))

// API routes with route groups
app.get("/", soul(req, res) {
    res.json({ 
        message: "Welcome to Jet API",
        version: "1.0.0",
        environment: app.get("env")
    })
})

// Authentication endpoints
app.post("/auth/login", soul(req, res) {
    // Basic authentication example
    if (req.body.username == "admin" && req.body.password == "secret") {
        res.json({ 
            token: "jwt-token-here",
            expiresIn: 3600,
            user: { id: 1, username: "admin" }
        })
    } else {
        res.status(401).json({ error: "Invalid credentials" })
    }
})

// Protected routes using fluent API
app.get("/api/users", soul(req, res) {
    res.json({ 
        users: [
            { id: 1, name: "Alice", email: "alice@example.com" },
            { id: 2, name: "Bob", email: "bob@example.com" }
        ]
    })
})
.description("Get all users")
.cache({ ttl: 300 })

// Health check endpoint
app.get("/health", soul(req, res) {
    res.json(app.health())
})

// Metrics endpoint (production monitoring)
app.get("/metrics", soul(req, res) {
    metrics = {
        requests: app.performance.requests,
        errors: app.performance.errors,
        avgResponseTime: app.performance.avgResponseTime,
        uptime: time.now() - app.performance.startTime,
        memory: {
            // Add memory usage if available
            used: "N/A"
        }
    }
    res.json(metrics)
})

// Global error handler
app.error(soul(error, req, res, next) {
    app.logger.error("Error: " + error.message)
    
    if (res.headersSent) {
        return next(error)
    }
    
    statusCode = error.status || 500
    message = app.get("env") == "production" ? "Internal Server Error" : error.message
    
    res.status(statusCode).json({
        error: message,
        timestamp: time.now()
    })
})

// Start server with production logging
app.setStartTime(time.now())
app.listen(soul() {
    app.logger.info("🚀 Jet server started on port " + app.port)
    app.logger.info("📍 Environment: " + app.get("env"))
    app.logger.info("🌐 Visit: http://localhost:" + app.port)
})
```

### With Middleware

```soul
import { createJet } from "soul-package/framework/jet.soul"

app = createJet(3000)

// Add middleware
app.use(app.cors())
app.use(app.helmet())
app.use(app.compression())

// Logging middleware
app.use(soul(req, res, next) {
    Console.log(`${req.method} ${req.path}`)
    next()
})

// Routes
app.get("/api/users", soul(req, res) {
    res.json({ users: ["Alice", "Bob"] })
})

app.listen()
```

### HTML Rendering

```soul
import { createJet } from "soul-package/framework/jet.soul"

app = createJet(3000)

// Configure views
app.setViewsPath("views")
app.setDefaultLayout("layout")
app.enableViewCache(false) // Disable cache in development

// Add custom template helper
app.helper("formatDate", soul(date) {
    return date.toLocaleDateString()
})

// Render template route
app.get("/", soul(req, res) {
    data = {
        title: "Welcome to Jet",
        message: "Hello from the template engine!",
        users: [
            { name: "Alice", email: "alice@example.com" },
            { name: "Bob", email: "bob@example.com" }
        ],
        currentDate: time.now()
    }

    // Render with layout
    html = app.render("home", data)
    res.html(html)
})

// Render without layout
app.get("/simple", soul(req, res) {
    html = app.render("simple", { name: "World" }, { layout: false })
    res.html(html)
})

app.listen()
```

#### Template Syntax

**Variable Interpolation:**

```html
<h1>{{title}}</h1>
<p>Welcome, {{user.name}}!</p>
```

**Template Helpers:**

```html
<p>Today is {{formatDate currentDate}}</p>
<p>{{if user.isAdmin "Admin User" "Regular User"}}</p>
```

**Loops:**

```html
<ul>
  {{each users "
  <li>{{@item.name}} - {{@item.email}}</li>
  "}}
</ul>
```

**Includes:**

```html
{{include "partials/header"}}
<main>Content here</main>
{{include "partials/footer"}}
```

**Layout Example** (`views/layouts/layout.html`):

```html
<!DOCTYPE html>
<html>
  <head>
    <title>{{title}}</title>
    <meta charset="utf-8" />
  </head>
  <body>
    <header>
      <h1>My Website</h1>
    </header>
    <main>{{body}}</main>
    <footer>
      <p>&copy; 2024 My Website</p>
    </footer>
  </body>
</html>
```

## 🛠️ API Reference

### Application

#### `createJet(port)`

Creates a new Jet application instance.

```soul
app = createJet(3000)
```

#### Configuration Methods

```soul
// Set configuration
app.set("env", "production")
app.set("trustProxy", true)

// Get configuration
env = app.get("env")

// Environment shorthand
app.env("development")
```

#### View Configuration

```soul
// Set views directory
app.setViewsPath("views")

// Set default layout
app.setDefaultLayout("layout")

// Enable/disable view caching
app.enableViewCache(true)

// Register custom template helpers
app.helper("formatDate", soul(date) {
    return date.toLocaleDateString()
})

app.helper("capitalize", soul(text) {
    return text.charAt(0).toUpperCase() + text.slice(1)
})
```

#### Template Rendering

```soul
// Render template with data
html = app.render("template-name", data)

// Render with options
html = app.render("template-name", data, {
    layout: "custom-layout"  // or false for no layout
})

// Render string template
html = app.renderString("<h1>{{title}}</h1>", { title: "Hello" })
```

#### Middleware

```soul
// Global middleware
app.use(middleware)

// Path-specific middleware
app.use("/api", middleware)

// Multiple middleware
app.use(middleware1, middleware2, middleware3)
```

#### Routing

```soul
// HTTP methods
app.get("/", handler)
app.post("/users", handler)
app.put("/users/:id", handler)
app.delete("/users/:id", handler)
app.patch("/users/:id", handler)
app.options("/users", handler)
app.head("/users", handler)

// All methods
app.all("/admin/*", handler)

// Route groups
app.group("/api/v1", soul(api) {
    api.get("/users", handler)
    api.post("/users", handler)
})
```

#### Route Builder (Fluent API)

```soul
app.get("/users/:id", handler)
   .middleware(auth, validate)
   .auth({ strategy: "jwt" })
   .validate({ params: { id: { type: "number" } } })
   .cache({ ttl: 300 })
   .rateLimit({ max: 100 })
   .description("Get user by ID")
   .tags("users", "public")
   .version("1.0.0")
```

#### Server Lifecycle

```soul
// Start server
app.listen(soul() {
    Console.log("Server started!")
})

// Graceful shutdown
app.close(soul() {
    Console.log("Server stopped!")
})
```

### Request Object

```soul
app.get("/users/:id", soul(req, res) {
    // Basic properties
    method = req.method        // "GET"
    path = req.path           // "/users/123"
    url = req.url             // Full URL

    // Headers
    userAgent = req.headers["user-agent"]
    contentType = req.headers["content-type"]

    // Parameters
    userId = req.params.id    // Path parameters
    search = req.query.search // Query parameters

    // Body (parsed automatically)
    data = req.body           // Request body
    jsonData = req.json       // Parsed JSON

    // Additional properties
    ip = req.ip              // Client IP
    secure = req.secure      // HTTPS check
    xhr = req.xhr            // AJAX request check

    // Authentication
    user = req.user          // Authenticated user
    authenticated = req.authenticated // Auth status

    // Utilities
    header = req.header("authorization")
})
```

### Response Object

```soul
app.get("/", soul(req, res) {
    // Status code
    res.status(200)
    res.status(201).json({ created: true })

    // Headers
    res.header("X-Custom", "value")
    res.header("Cache-Control", "no-cache")

    // Response methods
    res.json({ message: "Hello" })
    res.text("Plain text")
    res.html("<h1>Hello</h1>")
    res.send(data) // Auto-detect content type

    // Cookies
    res.cookie("name", "value", { httpOnly: true })
    res.clearCookie("name")

    // Redirects
    res.redirect("/login")
    res.redirect("/dashboard", 301)

    // File operations
    res.download("/path/to/file.pdf")
    res.sendFile("/path/to/file.html")

    // Template rendering
    res.render("template", { data: "value" })

    // End response
    res.end()
})
```

### Built-in Middleware

#### CORS Middleware

```soul
// Basic CORS
app.use(app.cors())

// Advanced CORS configuration
app.use(app.cors({
    origin: "*",                    // or specific domain
    methods: ["GET", "POST", "PUT", "DELETE", "PATCH", "OPTIONS"],
    headers: ["Content-Type", "Authorization"],
    credentials: false,
    maxAge: 86400,
    preflightContinue: false
}))
```

#### Security Headers (Helmet)

```soul
// Basic security headers
app.use(app.helmet())

// Custom security configuration
app.use(app.helmet({
    contentSecurityPolicy: true,    // CSP header
    frameguard: true,              // X-Frame-Options
    hidePoweredBy: true,           // Remove X-Powered-By
    noSniff: true,                 // X-Content-Type-Options
    xssFilter: true                // X-XSS-Protection
}))
```

#### Rate Limiting

```soul
// Basic rate limiting
app.use(app.rateLimit())

// Custom rate limiting
app.use(app.rateLimit({
    windowMs: 900000,              // 15 minutes
    max: 100,                      // Max requests per window
    message: "Too many requests"   // Error message
}))
```

#### Response Compression

```soul
// Basic compression
app.use(app.compression())

// Custom compression settings
app.use(app.compression({
    level: 6,                      // Compression level (1-9)
    threshold: 1024,               // Minimum size to compress
    filter: null                   // Custom filter function
}))
```

#### Static File Serving

```soul
// Serve static files from public directory
app.static("/static", "./public")

// Multiple static directories
app.static("/css", "./assets/css")
app.static("/js", "./assets/js")
app.static("/images", "./assets/images")
```

### Authentication

```soul
import { AuthPlugin } from "soul-package/framework/plugins/auth.soul"

// Install auth plugin
app.plugin(new AuthPlugin(), {
    jwtSecret: "your-secret-key",
    sessionMaxAge: 24 * 60 * 60 * 1000
})

// Authentication strategies
app.use(app.authenticate("jwt"))
app.use(app.authenticate("session"))
app.use(app.authenticate("basic"))
app.use(app.authenticate("apikey"))

// Authorization
app.use(app.authorize(["admin", "moderator"]))
app.use(app.requireRole("admin"))
app.use(app.requirePermission("write"))

// Login routes
app.login("/api/auth/login", "jwt")
app.register("/api/auth/register", "jwt")
app.logout("/api/auth/logout")
```

### Validation

```soul
import { ValidationPlugin } from "soul-package/framework/plugins/validation.soul"

// Install validation plugin
app.plugin(new ValidationPlugin())

// Validation middleware
app.post("/users",
    app.validate({
        body: {
            name: { required: true, type: "string", minLength: 2 },
            email: { required: true, type: "string", email: true },
            age: { type: "number", min: 18, max: 120 }
        }
    }),
    soul(req, res) {
        // Request is automatically validated
        user = req.body
        res.json({ user: user })
    }
)

// Custom validation rules
app.rule("strongPassword", soul(value) {
    return value.length() >= 8 && /[A-Z]/.test(value) && /[0-9]/.test(value)
})
```

### Database Integration

```soul
import { DatabasePlugin } from "soul-package/framework/plugins/database.soul"

// Install database plugin
app.plugin(new DatabasePlugin(), {
    connections: {
        main: {
            type: "postgres",
            host: "localhost",
            database: "myapp",
            user: "postgres",
            password: "password"
        }
    }
})

// Define models
User = app.model("User", {
    fields: {
        id: { type: "number", primaryKey: true },
        name: { type: "string", required: true },
        email: { type: "string", required: true, unique: true }
    }
})

// Use models
app.get("/users", soul(req, res) {
    users = User.find()
    res.json({ users: users })
})

app.post("/users", soul(req, res) {
    user = User.create(req.body)
    res.json({ user: user })
})
```

### Error Handling

```soul
// Custom error handler
app.error(soul(error, req, res, next) {
    Console.error("Error:", error.message)

    res.status(error.status or 500).json({
        error: error.message,
        stack: app.get("env") == "development" ? error.stack : undefined
    })
})

// Async error handling
app.get("/async", soul(req, res, next) {
    try {
        result = await someAsyncOperation()
        res.json({ result: result })
    } catch (error) {
        next(error)
    }
})
```

### Architecture Components

```soul
// Controller registration and usage
UserController = {
    login: soul(req, res) {
        // Authentication logic
        res.json({ token: "jwt-token", user: req.body.username })
    },
    register: soul(req, res) {
        // Registration logic  
        res.json({ success: true, user: req.body })
    }
}

app.registerController("UserController", UserController)

// Use controller in routes
app.post("/auth/login", app.controller("UserController", "login"))
app.post("/auth/register", app.controller("UserController", "register"))
```

```soul
// Service registration
UserService = {
    findUser: soul(id) {
        // User lookup logic
        return { id: id, name: "User " + id }
    }
}

app.registerService("UserService", UserService)

// Repository pattern
UserRepository = {
    save: soul(user) {
        // Save user logic
        return user
    }
}

app.registerRepository("UserRepository", UserRepository)
```

### Health Monitoring

```soul
// Built-in health check
app.get("/health", soul(req, res) {
    res.json(app.health())
})

// Performance metrics
app.get("/metrics", soul(req, res) {
    res.json({
        requests: app.performance.requests,
        errors: app.performance.errors,
        avgResponseTime: app.performance.avgResponseTime,
        startTime: app.performance.startTime
    })
})
```

## 📚 Examples

### Simple API

```soul
import { createJet } from "soul-package/framework/jet.soul"

app = createJet(3000)

app.get("/api/users", soul(req, res) {
    res.json({ users: ["Alice", "Bob"] })
})

app.post("/api/users", soul(req, res) {
    res.json({ user: req.body })
})

app.listen()
```

### Full-Featured API

```soul
import { createJet } from "soul-package/framework/jet.soul"
import { AuthPlugin } from "soul-package/framework/plugins/auth.soul"
import { ValidationPlugin } from "soul-package/framework/plugins/validation.soul"

app = createJet(3000)

// Install plugins
app.plugin(new AuthPlugin())
app.plugin(new ValidationPlugin())

// Global middleware
app.use(app.cors())
app.use(app.helmet())
app.use(app.rateLimit({ max: 100 }))

// Protected API group
app.group("/api/v1", soul(api) {
    api.use(app.authenticate("jwt"))

    api.get("/users", soul(req, res) {
        res.json({ users: [] })
    })

    api.post("/users",
        app.validate({
            body: {
                name: { required: true, type: "string" },
                email: { required: true, type: "string", email: true }
            }
        }),
        soul(req, res) {
            res.json({ user: req.body })
        }
    )
})

app.listen()
```

## 🔧 Configuration

### Environment Variables

```bash
# Server
PORT=3000
NODE_ENV=production

# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=myapp
DB_USER=postgres
DB_PASSWORD=password

# Authentication
JWT_SECRET=your-secret-key
SESSION_SECRET=session-secret

# Security
ALLOWED_ORIGINS=https://example.com,https://app.example.com
TRUST_PROXY=true
```

### Application Settings

```soul
// Environment
app.env("production")

// Trust proxy
app.set("trustProxy", true)

// Custom settings
app.set("uploadDir", "./uploads")
app.set("maxFileSize", 10 * 1024 * 1024)
```

## 🚀 Deployment

### Docker

```dockerfile
FROM soul-lang:latest

WORKDIR /app
COPY . .

EXPOSE 3000

CMD ["soul", "run", "app.soul"]
```

### Production

```soul
import { createJet } from "soul-package/framework/jet.soul"

app = createJet(process.env.PORT or 3000)

// Production configuration
app.env("production")
app.set("trustProxy", true)

// Security
app.use(app.helmet())
app.use(app.cors({
    origin: process.env.ALLOWED_ORIGINS.split(","),
    credentials: true
}))

// Error handling
app.error(soul(error, req, res, next) {
    // Log error to external service
    logger.error(error)

    res.status(500).json({
        error: "Internal Server Error"
    })
})

app.listen()
```

## 📖 Best Practices

### Project Structure

```
project/
├── app.soul              # Main application
├── routes/               # Route definitions
│   ├── api/
│   │   ├── users.soul
│   │   └── posts.soul
│   └── web.soul
├── middleware/           # Custom middleware
│   ├── auth.soul
│   └── validation.soul
├── models/              # Database models
│   ├── user.soul
│   └── post.soul
├── config/              # Configuration
│   ├── database.soul
│   └── app.soul
├── public/              # Static files
└── tests/               # Test files
```

### Code Organization

```soul
// routes/api/users.soul
export createUsersRouter = soul(app) {
    router = app.group("/users")

    router.get("/", getUsers)
    router.post("/", createUser)
    router.get("/:id", getUser)
    router.put("/:id", updateUser)
    router.delete("/:id", deleteUser)

    return router
}

// app.soul
import { createJet } from "soul-package/framework/jet.soul"
import { createUsersRouter } from "./routes/api/users.soul"

app = createJet(3000)

// Setup routes
app.group("/api/v1", soul(api) {
    createUsersRouter(api)
})

app.listen()
```

### Error Handling

```soul
// Global error handler
app.error(soul(error, req, res, next) {
    // Log error
    logger.error("Request error:", {
        error: error.message,
        stack: error.stack,
        request: {
            method: req.method,
            path: req.path,
            ip: req.ip
        }
    })

    // Send response
    if (error.status) {
        res.status(error.status).json({
            error: error.message
        })
    } else {
        res.status(500).json({
            error: "Internal Server Error"
        })
    }
})
```

### Testing

```soul
// tests/api.soul
import { createJet } from "soul-package/framework/jet.soul"

// Test helper
soul testRequest(app, method, path, data) {
    // Implementation would make actual HTTP request
    return {
        status: 200,
        body: { success: true }
    }
}

// Test cases
soul testAPI() {
    app = createJet(3001)

    app.get("/test", soul(req, res) {
        res.json({ message: "test" })
    })

    response = testRequest(app, "GET", "/test")
    assert(response.status == 200)
    assert(response.body.message == "test")

    Console.log("✅ All tests passed!")
}
```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- Inspired by Express.js, Gin, and other great web frameworks
- Built on the powerful Soul programming language
- Community-driven development and feedback

---

**Jet Framework** - Building the future of web development with Soul 🚀
