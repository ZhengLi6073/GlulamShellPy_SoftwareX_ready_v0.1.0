# GlulamShellPy_SoftwareX_ready_v0.1.0
# GlulamShellPy: Abaqus-Based Parametric Modelling of Glulam Single-Layer Latticed Shells with Semi-Rigid Joints

GlulamShellPy is an English, GitHub-ready release scaffold for Abaqus-based parametric modelling and nonlinear analysis of glulam single-layer latticed shells with connector-based semi-rigid joints. The software targets spherical dome geometry, rigid joint hub regions, truncated member segments, zero-length `CONN3D2` connectors, local Cartesian/Cardan connector components, geometric imperfections, static/Riks/buckling analysis workflows, and CSV post-processing of Abaqus ODB results.

## Motivation

Manual Abaqus modelling of semi-rigid latticed shell joints is repetitive and error-prone. The same assumptions must be kept consistent across joint topology, truncated member endpoints, local connector axes, connector stiffness data, boundary conditions, load cases, initial imperfections, analysis procedures, and ODB post-processing. GlulamShellPy provides a structured Python package, JSON configuration examples, and smoke tests so the modelling workflow can be reviewed, shared, and prepared for SoftwareX/GitHub publication.

## Main Features

- Parametric dome geometry for glulam single-layer latticed shells.
- Grid options represented in configuration: Kiewitt, Schwedler, lamella, three-way, and geodesic.
- Rigid hub plus truncated glulam member topology.
- `B31` beam member modelling.
- `CONN3D2` connector modelling with Cartesian/Cardan component conventions.
- Linear, nonlinear, free, and rigid connector component behaviours represented in JSON configuration.
- Direct geometric imperfections, member-level sinusoidal crookedness, and eigenmode-based imperfection workflow placeholders.
- Static, modified Riks, and linear buckling analysis workflow configuration.
- CSV-oriented post-processing structure for displacement, reactions, member forces/moments, and connector quantities.

## Installation

Non-Abaqus smoke tests use ordinary Python:

```bash
pip install -e .
pip install -r requirements.txt
python -m pytest -q
```

Actual Abaqus model generation, job submission, and ODB post-processing require a local licensed Abaqus/CAE installation. Abaqus Python is not installed through `pip` or conda.

## Quick Start

Run repository and configuration smoke tests:

```bash
python -m pytest -q
```

Run the no-Abaqus input-deck smoke writer:

```bash
python repo/src/glulamshellpy/abaqus_scripts/abaqus_entry.py --config examples/smoke_minimal_config.json --output runs/smoke --write-input-only
```

When Abaqus is available, the optional smoke test can be run through Abaqus/CAE:

```bash
abaqus cae noGUI=repo/src/glulamshellpy/abaqus_scripts/abaqus_entry.py -- --config examples/smoke_minimal_config.json --output runs/smoke --write-input-only
```

Launch the lightweight GUI:

```bash
python -m glulamshellpy gui
```

Build a Windows reviewer executable:

```bat
build_windows_exe.bat
```

The generated visual reviewer app is written to `reviewer_exe/GlulamShellPyReviewer.exe`. It can load the bundled smoke example, validate the JSON configuration, and write a minimal Abaqus input deck without requiring reviewers to use command-line Python. Full Abaqus analysis and ODB post-processing still require Abaqus/CAE.

Build the public English runtime executable:

```bat
build_public_exe.bat
```

The generated portable desktop application is written to `dist/GlulamShellPy_Portable/GlulamShellPy.exe`. It follows the original visual workflow more closely than the reviewer tool: it loads and saves model configurations, edits common modelling fields, calls Abaqus/CAE noGUI to generate input files, can submit Abaqus jobs, and can launch ODB post-processing when an ODB is available. This single-file EXE is the recommended artifact for external reviewers and users.

## Examples

- `examples/smoke_minimal_config.json`: smallest fast input-file generation case; not a formal analysis benchmark.
- `examples/riks_reference_config.json`: reference configuration for a modified Riks workflow.
- `examples/eigenmode_imperfection_config.json`: two-stage buckling plus imperfection workflow; run the buckling job before the main analysis.
- `examples/member_imperfection_config.json`: member-level sinusoidal crookedness workflow with fixed member endpoints.

## Smoke Tests

Tier 0 tests run without Abaqus and check repository structure, metadata, import isolation, example JSON loading, and absence of CJK text outside `docs/translation_map.md`.

Tier 1 is optional and checks whether Abaqus can run a minimal noGUI input-file generation workflow.

Tier 2 is optional and applies only when a sample ODB is available for post-processing.

These smoke tests verify software structure, configuration loading, input-file generation plumbing, and optional Abaqus invocation. They do not verify structural performance, experimental agreement, reliability, or design-code calibration.

## Code Metadata

The SoftwareX code metadata table is maintained in `docs/softwarex_code_metadata.md`.

## Reviewer EXE

See `docs/reviewer_exe.md` for the reviewer executable build and use notes.

## Public EXE

See `docs/public_exe.md` for the public English executable build and use notes.

## Limitations

This release scaffold does not claim completed experimental validation, reliability analysis, or design standard calibration. Before submission, authors should add validated benchmark cases, error metrics, Abaqus version details, operating environment details, and complete result figures/tables for the manuscript.

GitHub repository links, archived release links, reproducible capsule links, Zenodo DOI, manuscript identifiers, support email, C2, C3, and C9 remain `TBD` until the public release is created.

## Citation

Please use `CITATION.cff`. Repository and DOI fields are intentionally `TBD` until public archival release.

## License

This English release uses the license in `LICENSE.txt`. No existing license file was detected in the Chinese source root, so MIT License is provided as the default placeholder. Authors must confirm copyright ownership and final license choice before submission.
