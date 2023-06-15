This is not a bug, but an intended behavior according to the documentation (https://python-poetry.org/docs/repositories/#package-source-constraint)

The simplest way to resolve this is to add `foo_base` dependency definition with a wildcard version to `foo_app`'s pyproject.toml in a separate, explicit dependency group. Version constraint will derive from `foo` and poetry will know in what source to look for `foo_base`.
```
poetry add --group explicit --source pypi_foo foo_base@*
```

Result in the pyproject.toml:
```
[tool.poetry.group.explicit.dependencies]
foo-base = {version = "*", source = "pypi_foo"}
```
