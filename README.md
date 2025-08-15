# Schematra

<img src="public/logo-sm.png" alt="Schematra Logo"/>

*The web framework that makes complex things simple*

A modern web framework for [CHICKEN Scheme](https://call-cc.org/) that combines simplicity with power. Authentication in 3 lines. Middleware that's actually composable. HTML that looks like your data.

🌐 **[Visit schematra.com](https://schematra.com)** for interactive examples and live demos.

## Why Schematra?

- **Zero Config Sessions**: Cookie-based sessions work immediately. No setup, no database, no complexity
- **HTML as Data**: Write `[.card [h1 "Title"]]` instead of wrestling with template engines
- **3-Line Middleware**: Real middleware that composes. Write a function, call `use-middleware!`, done
- **Express in 50 Lines vs Schematra in 15**: What takes other frameworks dozens of lines takes Schematra a few

## Features

- Simple route definition with `get`, `post`, etc. functions
- URL parameter extraction and query parameter handling
- Middleware system with built-in session management
- Development mode with REPL integration
- [Hiccup](https://github.com/weavejester/hiccup)-inspired template system (Chiccup)
- Built on the solid [Spiffy](http://wiki.call-cc.org/eggref/5/spiffy) web server

## Quick Start

### Installation

```bash
git clone https://github.com/rolandoam/schematra
cd schematra
chicken-install
```

### Complete Web App

```scheme
(import schematra chiccup sessions)

(use-middleware! (session-middleware "secret-key"))

(get ("/")
     (let ((user (session-get "username")))
       (if user
           (ccup/html `[h1 ,(format "Welcome back, ~a!" user)])
           (redirect "/login"))))

(post ("/login")
      (let ((username (alist-ref 'username (current-params))))
        (session-set! "username" username)
        (redirect "/")))

(schematra-start)
```

Save as `app.scm`, run with `csi app.scm`, and visit `http://localhost:8080`.

## Documentation

For comprehensive documentation including:

- **[Getting Started Guide](docs/docs.md#getting-started)** - Installation, system requirements, and your first app
- **[Core Concepts](docs/docs.md#core-concepts)** - Routing, parameters, and request handling
- **[Chiccup Templating](docs/docs.md#chiccup-templating)** - HTML generation with Lisp syntax
- **[API Reference](docs/docs.md#api-reference)** - Complete function documentation
- **[Middleware System](docs/docs.md#middleware-system)** - Composable request/response processing
- **[Advanced Topics](docs/docs.md#advanced-topics)** - Sessions, static files, and deployment
- **[Examples & Recipes](docs/docs.md#examples--recipes)** - Common patterns and use cases

Visit the **[full documentation](docs/docs.md)**.

## Current Status

**This is an exploration project!** Schematra is in early development and not recommended for production use. It's perfect for:

- Learning Scheme and web development concepts
- Prototyping web applications
- Experimenting with functional web programming
- Understanding how web frameworks work

### What's Working
- ✅ Routing and parameter handling
- ✅ Middleware system
- ✅ Session management
- ✅ Chiccup HTML templating
- ✅ Development mode with REPL
- ✅ Static file serving

### What's Coming
- [ ] Enhanced error handling
- [ ] Database integration helpers
- [ ] WebSocket support
- [ ] Background job system
- [ ] Production deployment guides

## Contributing

Contributions welcome! See our [contributing guidelines](docs/docs.md#contributing) for:

- Reporting bugs and requesting features
- Code style and development setup
- Roadmap and planned features

## License

GNU General Public License v3.0 - see [LICENSE.md](LICENSE.md) for details.
