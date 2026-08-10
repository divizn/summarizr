# summarizr

Takes a YouTube video's transcript and summarizes it with AI.

This is a superproject that pins together the three independent repos that make up the project:

- [summarizr-model](https://github.com/divizn/summarizr-model) (private) — the ML side: transcript fetching, summarization, training data scraper, and fine-tuning notebooks
- [summarizr-api](https://github.com/divizn/summarizr-api) (private) — Go API that fronts the model service over HTTP
- [summarizr-webui](https://github.com/divizn/summarizr-webui) (private) — web UI, not started yet

Each is developed and versioned independently; this repo just tracks which commit of each is known to work together.
