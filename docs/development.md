# :hammer_and_wrench: Development

This project uses [Task](https://taskfile.dev/) as a command runner. The `Taskfile.yaml` at the root of the project contains all the available commands.

## :books: Documentation

The documentation is built using [MkDocs](https://www.mkdocs.org/) with the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

### :package: Dependencies

To install the documentation dependencies, run the following command:

```bash
task docs-deps
```

### :rocket: Local Development Server

To start a local development server that automatically reloads when you make changes, run:

```bash
task serve
```

This will make the documentation available at `http://localhost:8000`.

### :ship: Deployment

To deploy the documentation to GitHub Pages, run:

```bash
task docs-deploy
```
