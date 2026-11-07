---
title: "Portfolio CI/CD Pipeline"
summary: "A Jekyll portfolio with automated build checks and GitHub Pages deployment using GitHub Actions."
status: "Implemented"
order: 0
skills:
  - GitHub Actions
  - Jekyll
  - CI/CD
  - GitHub Pages
---

## Overview

This portfolio is also a practical DevOps project: its source code, site generation, validation, and deployment are maintained in GitHub.

**Source repository:** [josedjc-dev.github.io](https://github.com/josedjc-dev/josedjc-dev.github.io)

**Workflow definition:** [Jekyll CI/CD](https://github.com/josedjc-dev/josedjc-dev.github.io/blob/main/.github/workflows/jekyll.yml)

**Build and deployment history:** [GitHub Actions](https://github.com/josedjc-dev/josedjc-dev.github.io/actions)

## Architecture

```text
Feature branch → Pull request → CI checks
                                    │
                                    ▼
                              Merge into main
                                    │
                                    ▼
                          Build + HTML validation
                                    │
                                    ▼
                         GitHub Pages artifact
                                    │
                                    ▼
                         GitHub Pages deployment
```

The website uses Jekyll to generate static pages from Liquid templates and Markdown project documents. GitHub Actions runs the automated workflow, and GitHub Pages hosts the generated website.

## Continuous integration

The workflow runs on pull requests targeting `main` and on pushes to `main`. Its build job:

1. Checks out the repository.
2. Sets up Ruby 3.3 and installs dependencies with Bundler.
3. Builds the Jekyll site with `JEKYLL_ENV=production`.
4. Checks generated HTML and internal links with HTMLProofer.

External URL checks are disabled to avoid making site builds depend on third-party websites. The validation is a useful quality gate, not a complete accessibility or security audit.

## Continuous deployment

On pushes to `main`, a successful build uploads the generated `_site` directory as a GitHub Pages artifact. A separate deployment job publishes it using GitHub's Pages deployment action and scoped permissions.

Pull-request builds do **not** deploy to production. The existing live site therefore remains available while changes are reviewed.

## Operating the pipeline

- **Review changes:** create a feature branch and open a pull request.
- **Check quality:** review the Actions build and validation result.
- **Release:** merge approved changes into `main`.
- **Monitor:** inspect workflow and deployment logs in GitHub Actions; failure notifications are configured in GitHub account settings.

## Implementation notes and next improvements

This implementation has been deployed successfully to GitHub Pages. Future improvements could include dependency pinning with a committed lockfile, Dependabot updates, branch protection, automated accessibility testing, and more granular validation.

The pipeline runs entirely on GitHub-hosted infrastructure; it does not provision Azure resources. Azure infrastructure as code is tracked as a separate planned project.
