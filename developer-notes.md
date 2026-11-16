# Developer Notes
This documents contains notes for developers working on the project.

## Compiling and Testing

In order to compile the project, first create a Python virtual environment and install dependencies:

```
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r docs/requirements.txt
```

> [!NOTE]
> If you are on Windows, activate the virtual environment with:
> ```
> .venv\Scripts\activate
> ```

Then build the docs:

- macOS/Linux:

```
make -C docs html
```

- Windows:

```
cd docs
.\make.bat html
```

This will generate the HTML files in the `docs/_build/html` directory.

To test the compiled HTML files, you can run a local web server using Python:

```
cd docs
python -m http.server --bind localhost --directory _build/html
```

This will start a web server on `http://localhost:8000` where you can view the compiled documentation.

## Publishing

The documentation gets automatically published on Read the Docs when a new tag is pushed to the repository.

TODO - add link to Read the Docs once it's set up.
