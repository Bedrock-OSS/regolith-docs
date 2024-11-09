# Developer Notes
This documents contains notes for developers working on the project.

## Compiling and Testing

In order to compile the project, simply `cd` into the `docs` directory and run the build script:

```
cd docs
./build.bat html
```

This will generate the HTML files in the `docs/_build/html` directory.

To test the compiled HTML files, you can run a local web server using Python:

```
cd docs
python -m http.server --bind localhost -d .\_build\html\
```

This will start a web server on `http://localhost:8000` where you can view the compiled documentation.

## Publishing

The documentation gets automatically published on Read the Docs when a new tag is pushed to the repository.

TODO - add link to Read the Docs once it's set up.
