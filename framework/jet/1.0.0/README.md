# Jet Framework

A modern, powerful, and feature-rich web framework for the Soul programming language. Jet is inspired by Express.js and other popular web frameworks, but built specifically for Soul with advanced features like built-in authentication, validation, database integration, and real-time capabilities.

## 🚀 Features

### Core Features

- **Fast HTTP Server** - Built on Soul's HTTP module with excellent performance
- **Flexible Routing** - Support for path parameters, query strings, and route groups
- **Middleware System** - Composable middleware with built-in and custom options
- **Method Chaining** - Fluent API for clean, readable code
- **Error Handling** - Comprehensive error handling with custom error pages
- **Static File Serving** - Built-in static file server with caching
- **HTML Template Engine** - Built-in template engine with layouts, partials, and helpers
- **Request/Response Helpers** - Rich API for handling HTTP requests and responses

### Advanced Features

- **Authentication System** - JWT, Session, Basic Auth, and API Key strategies
- **Authorization** - Role-based and permission-based access control
- **Validation Engine** - Comprehensive request validation with custom rules
- **Database Integration** - Multi-database support with ORM-like features
- **Real-time Support** - WebSocket integration for real-time features
- **Caching** - Multiple caching strategies and adapters
- **Rate Limiting** - Configurable rate limiting with multiple strategies
- **Security Headers** - Built-in security middleware (Helmet equivalent)
- **CORS Support** - Flexible Cross-Origin Resource Sharing
- **Compression** - Response compression with multiple algorithms
- **Logging** - Structured logging with request tracking
- **Metrics** - Built-in performance monitoring and metrics
- **Plugin System** - Extensible architecture with custom plugins
- **Hook System** - Lifecycle hooks for custom logic
- **OpenAPI Generation** - Automatic API documentation generation

## 📦 Installation

```bash
# Clone the Soul framework
git clone https://github.com/soul-lang/soul-package
cd soul-package/framework

# Or include in your Soul project
import { createJet } from "soul-package/framework/jet.soul"
```

## 🏃‍♂️ Quick Start

### Basic Server

```soul
import { createJet } from "soul-package/framework/jet.soul"

// Create app
app = createJet(3000)

// Basic route
app.get("/", soul(req, res) {
    res.json({ message: "Hello from Jet!" })
})

// Start server
app.listen(soul() {
    Console.log("🚀 Server running on port 3000")
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

#### Security

```soul
// CORS
app.use(app.cors({
    origin: "https://example.com",
    methods: ["GET", "POST"],
    headers: ["Content-Type", "Authorization"],
    credentials: true
}))

// Security headers
app.use(app.helmet({
    contentSecurityPolicy: true,
    frameguard: true,
    hsts: true
}))

// Rate limiting
app.use(app.rateLimit({
    windowMs: 15 * 60 * 1000, // 15 minutes
    max: 100, // limit each IP to 100 requests per windowMs
    message: "Too many requests"
}))
```

#### Utilities

```soul
// Compression
app.use(app.compression({
    level: 6,
    threshold: 1024
}))

// Static files
app.use("/static", app.static("./public", {
    maxAge: 86400000, // 1 day
    etag: true
}))

// Body parsing (automatic)
app.use(soul(req, res, next) {
    // JSON parsing is automatic
    data = req.json
    next()
})
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

### Plugins

```soul
// Create custom plugin
MyPlugin = {
    install: soul(app, options) {
        app.myFeature = soul() {
            return "Custom feature"
        }
    }
}

// Use plugin
app.plugin(MyPlugin, { option: "value" })
```

### Hooks

```soul
// Lifecycle hooks
app.hook("beforeStart", soul(app) {
    Console.log("Server starting...")
})

app.hook("afterStart", soul(app) {
    Console.log("Server started!")
})

app.hook("beforeStop", soul(app) {
    Console.log("Server stopping...")
})

app.hook("afterStop", soul(app) {
    Console.log("Server stopped!")
})
```

### Monitoring

```soul
// Health check
app.get("/health", soul(req, res) {
    res.json(app.health())
})

// Metrics
app.get("/metrics", soul(req, res) {
    res.json({
        requests: app.performance.requests,
        errors: app.performance.errors,
        uptime: Date.now() - app.performance.startTime
    })
})

// OpenAPI documentation
app.get("/api/docs", soul(req, res) {
    res.json(app.openapi())
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
