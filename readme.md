# Actions TestPyPI

Repo for testing/prototyping github actions workflows which publish packages to (test) pypi.

This is in advance of setting this up for a real python package which will publish to real testpypi, without breaking anything related to the real package(s).

This was using the following guide from the Python Packaging User guide:

https://packaging.python.org/en/latest/guides/publishing-package-distribution-releases-using-github-actions-ci-cd-workflows/

If the current testpypi includes a copy of the package, it should be installable via:

```bash
python3 -m pip install --index-url https://test.pypi.org/simple/ ptheywoodtestpypi
```


Things Tested:

- Regular happy-path tags
- tags which do not start with `v` do not attempt an upload
- tag version does not need to match the pyproject.toml version. This is OK but could lead to errors (but an incorrect pushed tag is semi-problematic anyway)
- if a version number is already on pypi, another tag using the same version is rejected (with `HTTPError: 400 Bad Request from https://test.pypi.org/legacy/`), in which case the verison number must be changed (patch bump) and pushed as a separate tag.
- force pushing a tag triggers the workflow again
