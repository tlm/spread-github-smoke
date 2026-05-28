# spread-github smoke

A minimal spread project used to exercise the spread-github composite
action end-to-end against GitHub Actions.

## Layout

- `spread.yaml` — one lxd backend, ubuntu-24.04 system.
- `tests/passing/` — task that always succeeds.
- `tests/failing/` — task that always fails.
- `.github/workflows/spread.yml` — workflow that provisions lxd and invokes
  the spread-github action, pinned to the `spread-events` branch of
  `tlm/spread`.

## Usage

This directory is a self-contained git repo. To exercise it:

```
cd smoke
git init
git add .
git commit -m "initial"
git remote add origin git@github.com:tlm/spread-github-smoke.git
git push -u origin main
```

Then watch the Actions tab. The workflow should produce two GitHub Check
Runs (one `success`, one `failure`), each named after its spread task id.

## What it verifies

- The composite action installs spread-github at the pinned ref.
- spread-github reads the spread event stream and POSTs/PATCHes Check Runs.
- The pass and fail task outcomes map to the right Check Run conclusions.
- spread's stdout still passes through to the workflow's log.

PR smoke check trigger.
