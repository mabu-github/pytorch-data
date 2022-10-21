# Title

[RFC] Verify that the docs contain working code and self-contained examples using doctest

# 🚀 The feature

Currently there does not seem to be an automatic way to verify that the examples in the documentation are actually
working. This leads to issues like ([#433](https://github.com/pytorch/data/issues/433)).

An example should also be complete enough so that developers can easily try out the code.

A solution could be to use the sphinx doctest extension to test the documentation before building it. Docstrings can be
continuously migrated from standard reST doctests to test code that runs using the sphinx doctest extension.

# Motivation, pitch

Working examples that are up-to-date boost adoption of the library and make it easier for developers to become
proficient in using the library.

Therefore one could consider using doctest in order to be forced to write self-contained examples that execute without
error.

# Alternatives

Doctests can be executed in different ways:

-   Invoking plain python to execute the doctests as described [here](https://docs.python.org/3/library/doctest.html)
-   Using [pytest --doctest](https://docs.pytest.org/en/7.1.x/how-to/doctest.html) to execute the tests
-   Run within the documentation build process as `cd docs && make doctest`

I would recommend running the doctests while building the documentation using sphinx because it is easy to continuously
migrate the existing non-tested example code to code being tested.

# Additional context

A minimal example of the RFC can be found
[here](https://github.com/pytorch/data/compare/main...mabu-github:pytorch-data:feature/rfc-doctest?expand=1). Please
note that the code is only meant as an example for discussion and does not (yet) meet the quality criteria of a PR.

The example implementation consists of the following parts:

-   An updated `docs/Makefile` with a `doctest` target
-   Enabling the sphinx extension `sphinx.ext.doctest` in `docs/source/conf.py`
-   A minimal example of an updated docstring in `torchdata/dataloader2/adapter.py`
-   Adding the `doctest` step to the CI in `.github/workflows/_build_test_upload.yml`

The tests can be executed like this: `cd docs && make doctest`.
