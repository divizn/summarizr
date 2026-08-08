# summarizr

Takes a YouTube video's transcript and summarizes it with AI.

This is a superproject that pins together the three independent repos that make up the project:

- [summarizr-model](https://github.com/divizn/summarizr-model) (private) — the ML side: transcript fetching, summarization, training data scraper, and fine-tuning notebooks
- [summarizr-api](https://github.com/divizn/summarizr-api) (private) — Go API that fronts the model service over HTTP
- [summarizr-webui](https://github.com/divizn/summarizr-webui) (private) — web UI, not started yet

Each is developed and versioned independently; this repo just tracks which commit of each is known to work together.

## Getting the code

```bash
git clone --recurse-submodules https://github.com/divizn/summarizr.git
```

If you already cloned without `--recurse-submodules`:

```bash
git submodule update --init --recursive
```

## Working across repos

Each subdirectory is a normal git checkout of its own repo, in detached HEAD by default. To make changes:

```bash
cd summarizr-api
git checkout main
# make changes, commit, push as usual
cd ..
git add summarizr-api
git commit -m "chore: bump summarizr-api"
```

Bumping the pointer in `summarizr` is how this repo tracks "known-good" combinations of the three — push the submodule's own commit first, then commit the pointer bump here.

## Local dev

See each repo's own README for setup. Typical order: start `summarizr-model` (`make model-serve`), then `summarizr-api` (`make api-run`), pointing `MODEL_API_URL` at the model service.

## Deployment

Local inference on CPU is slow (~15 minutes per summary), so `summarizr-api/terraform/` has an on-demand GPU deployment (single EC2 instance, Docker Compose, start/stop via `make aws-up`/`make aws-down`) — see that repo's README for setup. Not yet applied to real AWS infrastructure.
