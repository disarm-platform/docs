# Copying an existing algorithm

A new algo needs to have:

- `../Dockerfile` - copied from existing
- `requirements.txt` - copied from existing
- `/index.py` - copied from existing
- `/config.py` - copied from existing
- `/preprocess_helpers.py` - copied from existing
- `/function/handler.py` - with a function called `run_function`
- `/function/preprocess_params.py` - with tests for EVERY param in `SPECS.md`, can optionally use the helpers in `preprocess_helpers.py`
