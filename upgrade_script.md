# PyPI Package Update Guide

## Updating the Package Version

1. Update version number in `setup.cfg`:
```ini
[metadata]
version = X.Y.Z  # Increment this
```

2. Clean old build artifacts:
```bash
rm -rf dist/
rm -rf build/
rm -rf src/*.egg-info
rm -rf *.egg-info
```

3. Build new version:
```bash
python -m build
```

4. Upload to PyPI (only new version):
```bash
python -m twine upload dist/beeminder_client-X.Y.Z*
```

5. Test installation:
```bash
pip uninstall beeminder-client
pip install --no-cache-dir beeminder-client
```

## Version Numbering Guidelines
- For bug fixes: increment Z (0.1.0 -> 0.1.1)
- For new features: increment Y (0.1.1 -> 0.2.0)
- For breaking changes: increment X (0.2.0 -> 1.0.0)

## Common Issues
- Always use relative imports in your code (e.g., `from .models import X`)
- Cannot reuse version numbers on PyPI
- If upload fails, check you're not trying to upload an existing version
- Use `--no-cache-dir` when testing to ensure you get the latest version

## Quick Command Reference
```bash
# One-liner for update
rm -rf dist/ build/ *.egg-info src/*.egg-info && python -m build && python -m twine upload "dist/beeminder_client-*"

# Test install
pip install --no-cache-dir beeminder-client
```