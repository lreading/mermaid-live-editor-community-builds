# mermaid-live-editor-community-builds

Community-maintained container images of the Mermaid Live Editor with alternative build configurations.  
This repository is **not affiliated with** and **not an official Mermaid project**.

These images are built from upstream releases of the Mermaid Live Editor with specific build-time settings to adjust UI integration with external services.

---

## Upstream project

This project builds variants of the official Mermaid Live Editor frontend:

- GitHub repo: https://github.com/mermaid-js/mermaid-live-editor
- Upstream build configuration documentation: https://github.com/mermaid-js/mermaid-live-editor#build-args

Review those for additional context on the build arguments used here.

---

## Build configuration variables

***All*** image variants in this repo are built with the following overrides relative to upstream defaults:

| Build variable | Purpose |
|---------------|---------|
| `MERMAID_ANALYTICS_URL=""` | Disables analytics (upstream default is already off, but set explicitly here) |
| `MERMAID_DOMAIN=""` | Domain used for analytics attribution; irrelevant if analytics is disabled |
| `MERMAID_IS_ENABLED_MERMAID_CHART_LINKS=""` | Disables the Mermaid Chart/mermaid.ai links |


---

## Available image tags

Each variant includes the above default buid-args, as well as the specific build-args configuration for that variant.

| Tag suffix | Description | Build-time config |
|------------|-------------|------------------|
| `-nocloud` | Minimal external integrations. No renderer UI action and no Kroki UI action. | `MERMAID_RENDERER_URL=""`<br>`MERMAID_KROKI_RENDERER_URL=""` |
| `-kroki-default` | Enables the public Kroki integration in the UI; no external renderer UI action. | (default Kroki behavior)<br>`MERMAID_RENDERER_URL=""` |
| `-renderer-default` | Enables the public external renderer in the UI; no Kroki UI action. | (default render behavior)<br>`MERMAID_KROKI_RENDERER_URL=""` |
| `-kroki-renderer-default` | Enables both the public Kroki integration and the public external renderer UI actions. | (default behavior for both) |


Examples:
- `ghcr.io/lreading/mermaid-live-editor-community-builds:nocloud`
- `ghcr.io/lreading/mermaid-live-editor-community-builds:kroki-default`
- `ghcr.io/lreading/mermaid-live-editor-community-builds:renderer-default`
- `ghcr.io/lreading/mermaid-live-editor-community-builds:kroki-renderer-default`

---

## Release policy

This repository publishes automated releases and container images based off of the `master` branch of the official mermaid-live-editor repository, which is how Mermaid-Js builds/releases the official docker image.

Mermaid does not provide versioning information for the live-editor, and only really maintain a `latest` tag.  For that reason, we also cannot include version information in the tags.  Assume all variants/tags are "latest".

---

## Contributing

Community contributions are welcome!

If you want to introduce a new build variant:
- The variant must be enabled via documented upstream build arguments
- It should be generally useful to others
- Please do not add configurations that hardcode private or environment-specific values
- Update the GitHub Actions workflow to build and publish the new variant
- Add the variant to the tag table above with its description and build-time config

---

## Disclaimer

This is an unofficial community project. Mermaid and related trademarks belong to their respective owners. If you want the official experience, use the upstream images provided by the Mermaid project.

