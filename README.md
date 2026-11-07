# Jose de Jesus Castillo — portfolio and CI/CD

Public portfolio: https://josedjc-dev.github.io

This repository is a **Jekyll static site** with a **GitHub Actions CI/CD pipeline**. It showcases established experience in cloud infrastructure, enterprise architecture, and DevOps while documenting emerging data engineering and MLOps skills.

## Architecture

- **Source:** Jekyll pages, Liquid templates, Markdown project collection, CSS, and JavaScript.
- **CI:** Pull requests to `main` install dependencies, build the site, and validate generated HTML using HTMLProofer.
- **CD:** Pushes to `main` rebuild and validate, then publish the generated `_site` directory through GitHub Pages Actions.
- **Hosting:** GitHub Pages; no application server or database.

## Local development

Requires Ruby 3.3 and Bundler.

```sh
bundle install
bundle exec jekyll serve
```

Open http://127.0.0.1:4000.

Run the production checks locally:

```sh
JEKYLL_ENV=production bundle exec jekyll build
bundle exec htmlproofer ./_site --disable-external --allow-hash-href
```

## Deployment setup

1. In **Settings → Pages → Build and deployment**, change **Source** to **GitHub Actions**.
2. Merge a validated pull request into `main` to trigger the first automated deployment.
3. View deployment results in the repository's **Actions** tab.

**Important:** Switching the Pages source to GitHub Actions is a one-time repository setting. Keep the existing branch-based site live until the migration pull request is ready to merge.

## Content management

- `index.html`: homepage (Jekyll/Liquid).
- `_includes/`: shared navigation and footer.
- `_layouts/project.html`: reusable project detail layout.
- `_projects/*.md`: individual project pages and metadata.
- `_config.yml`: Jekyll configuration.
- `.github/workflows/jekyll.yml`: automated build, validation, and deployment.

To add a project, create a Markdown file in `_projects/` with `title`, `summary`, `status`, `order`, and `skills` front matter. The homepage generates project cards automatically.

## Roadmap

- Add an online résumé and downloadable PDF.
- Replace planned project entries with completed, linked implementations.
- Add tests, dependency monitoring, and further accessibility checks.
- Consider protected branches and required PR checks once CI is stable.

The initial project pages are clearly marked **Planned**. They are not presented as completed professional work.
