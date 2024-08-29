# `uv sync` does not install a member's dependency with extra

## Reproduction steps

1. Clone this repository
2. Run `uv sync` in the repository root
3. Run `uv pip list` in the repository root. It will only show `a-lib`
4. Run `uv run python -c "import httpx"` in the repository root. It will fail with `ModuleNotFoundError: No module named 'httpx'`

## Expected behavior

- `uv sync` should install `httpx` as:
  - `httpx` is in the `network` extra of `a-lib`
  - `a-lib[network]` is a dependency of `an-app`, which is a workspace member

## Other notes

- If you remove the `project.optional-dependencies` section from `a-lib/pyproject.toml` and run `uv add httpx --optional network`, it _will_ install `httpx` as expected. However, running `uv sync` will remove `httpx` again.
