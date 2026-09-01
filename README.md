# census_income

A starting point for a **census-income machine-learning project**. The repository description identifies the intended direction as deploying a machine-learning model with **FastAPI** on **Heroku**.

> **Repository status:** this revision contains only DVC scaffolding and plot templates. The dataset, training code, model, API, deployment files, and automated tests have not yet been added.

## What is in the repository?

The project is initialized for [DVC](https://dvc.org/), but no data or pipeline is currently tracked:

| Path | Purpose |
| --- | --- |
| `.dvc/config` | Project-level DVC configuration. It is currently empty, so no data remote is configured. |
| `.dvc/.gitignore` | Keeps DVC machine-local files such as the cache, temporary files, and local configuration out of Git. |
| `.dvc/plots/` | Vega-Lite v4 templates for visualizing DVC metrics and plots. |
| `.dvcignore` | Patterns for files DVC should ignore while scanning the workspace. |

The available plot templates are:

- `default.json` — a basic line chart
- `linear.json` — an interactive line chart with point labels
- `scatter.json` — an interactive scatter plot with point labels
- `smooth.json` — a LOESS-smoothed line chart
- `confusion.json` — a confusion-matrix heatmap showing counts
- `confusion_normalized.json` — a row-normalized confusion-matrix heatmap

These are reusable DVC templates rather than project results. They contain DVC placeholders such as `<DVC_METRIC_DATA>` and `<DVC_METRIC_X>` that are filled when a plot is rendered through DVC.

## Getting started

Clone the repository and inspect its current state:

```bash
git clone https://github.com/DawidGalarowicz/census_income.git
cd census_income
git status
```

To work with the DVC metadata, install DVC using the [official installation instructions](https://dvc.org/doc/install). There is no dependency lockfile or Python package manifest in this revision, so application-specific dependencies will need to be added as the project is built.

### Adding data with DVC

When a source dataset is available, it can be tracked without committing the data itself:

```bash
# Example only; replace the path with the real dataset.
dvc add data/census_income.csv

git add data/census_income.csv.dvc data/.gitignore
git commit -m "Track census income dataset with DVC"
```

A DVC remote must be configured before data can be shared with other clones. For example:

```bash
# Replace this with an approved shared storage location.
dvc remote add -d storage <remote-url>
dvc push
```

Do not commit credentials or machine-local DVC configuration. The repository's `.dvc/.gitignore` already excludes DVC's local cache and configuration files.

### Rendering DVC plots

After metrics or plot data have been produced, a template can be selected with DVC, for example:

```bash
dvc plots show --template .dvc/plots/default.json
```

The current repository does not yet contain a `dvc.yaml`, metrics file, or experiment output, so there is no project plot to render yet.

## Planned project components

To turn this scaffold into the intended end-to-end application, the project still needs:

1. A documented census-income dataset, schema, and data versioning workflow.
2. Reproducible preprocessing and model-training stages, ideally described in `dvc.yaml`.
3. Versioned metrics, plots, and a model evaluation report.
4. A FastAPI application that loads the trained model and validates prediction input.
5. Tests for preprocessing, model behavior, and API endpoints.
6. Dependency and deployment configuration for the target hosting platform.

Until those components are committed, this repository should be treated as a DVC-ready project skeleton rather than a runnable API or trained-model release.

## License

No license has been declared in the repository yet.
