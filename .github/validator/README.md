# Validator Image Wrapper

This directory contains a tiny Docker wrapper used by the GitHub Actions
workflows.

Why it exists:

- The workflows pin `ghcr.io/validator/validator` by digest for reproducibility.
- Dependabot does not update `docker://` image references in workflow files.
- Dependabot can update `FROM ...@sha256:...` in a Dockerfile when the
  `docker` ecosystem is configured.

How it is used:

- The workflows build this Dockerfile as `local/validator:latest`.
- They run `vnu` from that local image against the repository checkout.
- The repository is mounted read-only during validation.
