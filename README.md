# License Report Action

A GitHub Action for generating a complete `licenses.txt` file for Node.js projects (npm / React / Next.js / Vite / etc.).  
It combines:

- automatically detected third-party licenses via **license-checker-rseidelsohn**
- an optional manually maintained **licenses.txt** in the project root  
  → this file is **prepended** to the generated license report

Perfect for CI/CD pipelines, compliance reporting, and software distribution workflows.

---

## Usage Example (GitHub Actions)

```yaml
name: Generate Licenses

on:
  push:
    branches: [ main ]

jobs:
  generate-licenses:
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: "npm"

      - name: Install dependencies
        run: npm ci

      - name: Generate licenses.txt
        uses: durablox/license-report-action@v1
        # optional:
        # with:
        #   project-root: .
```

This will generate a consolidated `dist/licenses.txt` containing:
1. Your custom `licenses.txt` (if present in the project root)  
2. All detected third-party licenses

---

## License

This project is licensed under the **MIT License**.
