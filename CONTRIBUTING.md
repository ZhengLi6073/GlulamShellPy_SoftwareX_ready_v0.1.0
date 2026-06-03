# Contributing

Contributions should keep the English release import-safe in ordinary Python. Modules that require Abaqus-only APIs must isolate those imports inside Abaqus-specific entry points or functions.

Before submitting changes, run:

```bash
python -m pytest -q
python scripts/check_no_chinese.py
python scripts/make_release_zip.py
```

Do not commit Abaqus result files, caches, temporary folders, or generated release archives.

