# :hammer_and_wrench: Development

This project uses [Task](https://taskfile.dev/) as a command runner. The `Taskfile.yaml` at the root of the project contains all the available commands.

## :books: Documentation

The documentation is built using [MkDocs](https://www.mkdocs.org/) with the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

### :package: Dependencies

To install the documentation dependencies, run the following command:

=== "Task"

    ```bash
    task docs-deps
    ```

=== "Manual"

    ```bash
    pipx install mkdocs
    pipx install mkdocs-material
    pipx install pymdown-extensions
    ```

### :rocket: Local Development Server

To start a local development server that automatically reloads when you make changes, run:

=== "Task"

    ```bash
    task serve
    ```

=== "Manual"

    ```bash
     docker run --rm -it -p 8000:8000 -v ${PWD}:/docs \
        --platform linux/amd64 nicholaswilde/mkdocs-material serve \
        --dev-addr 0.0.0.0:8000 -f ./mkdocs.yml
    ```

This will make the documentation available at `http://localhost:8000`.

### :ship: Deployment

To deploy the documentation to GitHub Pages, run:

=== "Task"

    ```bash
    task docs-deploy
    ```

=== "Manual"

    ```bash
    mkdocs gh-deploy --force
    ```
