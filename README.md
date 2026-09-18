# mustache

[![CI](https://github.com/alya-lang/mustache/actions/workflows/ci.yml/badge.svg)](https://github.com/alya-lang/mustache/actions/workflows/ci.yml)
[![License](https://img.shields.io/github/license/alya-lang/mustache?color=blue&label=License)](LICENSE)
[![Alya](https://img.shields.io/badge/dynamic/toml?url=https%3A%2F%2Fraw.githubusercontent.com%2Falya-lang%2Fmustache%2Fmain%2Falya.toml&query=%24.package.alya-version&label=Alya&color=orange&prefix=%3E%3D)](https://github.com/alya-lang/alya)
[![Package Version](https://img.shields.io/badge/dynamic/toml?url=https%3A%2F%2Fraw.githubusercontent.com%2Falya-lang%2Fmustache%2Fmain%2Falya.toml&query=%24.package.version&label=Version&color=brightgreen)](alya.toml)

Fast, zero-dependency Mustache template engine for Alya

---

## 🌟 Features

- ⚡ **Lightweight & Fast**: Pure native Alya implementation processing over 1,000,000 templates/second with zero external dependencies
- 🧩 **Full Specification**: Supports variables (`{{var}}`), unescaped HTML (`{{{var}}}` & `{{&var}}`), loops and sections (`{{#sec}}`), inverted sections (`{{^sec}}`), comments (`{{!comment}}`), and partials (`{{>partial}}`)
- 🔍 **Dot Notation & Implicit Iterator**: Supports nested object path navigation (`{{user.profile.name}}`) and array scalar iteration (`{{.}}`)
- 🛡️ **Safe & Sanitized**: Built-in HTML escaping (`&`, `<`, `>`, `"`, `'`) with roundtrip unescaping support
- 🧪 **Well Tested**: Comprehensive unit test suite, micro-benchmarks, and realistic examples

---

## 📁 Project Architecture

```
mustache/
├── alya.toml               # Package manifest
├── src/
│   ├── lib.alya            # Public API facade
│   ├── types.alya          # AST nodes, template struct & tag constants
│   ├── escape.alya         # HTML entity sanitization & decoding
│   ├── context.alya        # Scope stack, key resolution & type introspection
│   ├── parser.alya         # Lexer and recursive AST builder
│   └── renderer.alya       # Template evaluator & partial resolver
├── examples/
│   └── demo.alya           # E-commerce store view template demo
├── tests/
│   ├── test_basic.alya     # Variable replacement & escaping tests
│   ├── test_sections.alya  # Section loops & inverted section tests
│   ├── test_partials.alya  # Partial inclusion & comment tests
│   └── test_escape.alya    # HTML entity encode/decode unit tests
└── benches/
    └── bench_basic.alya    # Compilation & rendering micro-benchmarks
```

> [!NOTE]
> **Modular Source:** Modules are cleanly separated inside `src/` (`types.alya`, `escape.alya`, `context.alya`, `parser.alya`, `renderer.alya`) and unified under the `src/lib.alya` facade for zero-overhead imports.

---

## 📦 Installation

Add `mustache` to the `[dependencies]` section in your `alya.toml`:

```toml
[dependencies]
mustache = { git = "https://github.com/alya-lang/mustache", branch = "main" }
```

Or install it directly using the Alya package CLI:

```bash
alya add mustache --git https://github.com/alya-lang/mustache --branch main
alya install
```

---

## 🚀 Quick Start

```alya
import "mustache" as mustache

function main()
    let tmpl = "Hello, {{name}}!\n"
    tmpl += "{{#items}} - {{.}}\n{{/items}}"
    tmpl += "{{^items}}No items found.{{/items}}"

    let data = {
        "name": "Developer",
        "items": ["Alya", "Mustache", "Speed"]
    }

    let output = mustache::render(tmpl, data)
    say output
end

main()
```

---

## 📖 API Reference

| Function | Arguments | Returns | Description |
|---|---|---|---|
| `render(template, data, partials)` | `template: string, data: map, partials = {}` | `string` | Parses template and renders output using data context and optional partials. |
| `compile(template)` | `template: string` | `Template` | Parses template string into an AST `Template` struct for reuse. |
| `render_template(compiled, data, partials)` | `compiled: Template, data: map, partials = {}` | `string` | Renders a precompiled `Template` struct with data and partials. |
| `render_file(path, data, partials)` | `path: string, data: map, partials = {}` | `string` | Reads a template file from disk and renders it with data and partials. |
| `escape_html(text)` | `text: string` | `string` | Escapes special HTML characters (`&`, `<`, `>`, `"`, `'`). |
| `unescape_html(text)` | `text: string` | `string` | Unescapes standard HTML entities back to raw characters. |

---

## 🧪 Running Tests & Benchmarks

Run the test suite using `alya`:

```bash
alya test
```

Run the benchmark suite:

```bash
alya run benches/bench_basic.alya
```

Run the example demo:

```bash
alya run examples/demo.alya
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository and clone it locally
2. Install dependencies:
   ```bash
   alya install
   ```
3. Create your feature branch (`git checkout -b feature/my-feature`)
4. Verify tests and formatting before opening a PR:
   ```bash
   alya test
   alya fmt . --check
   ```
5. Commit your changes (`git commit -m "feat: add feature"`) and open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.