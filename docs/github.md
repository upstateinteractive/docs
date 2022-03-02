# Github

## Table of Contents

## Automation with Issue Ticket and Pull Request Templates

GitHub provides the ability to generate pull request and issue ticket templates to encourage consensus of code style, purpose of changes and structuring issues. 

The enclosed `github` folder provides examples of a [pull request template](./github/PULL_REQUEST_TEMPLATE.md), a [bug issue ticket template](./github/ISSUE_TEMPLATE/BUG.md), and a [feature issue ticket template](./github/ISSUE_TEMPLATE/FEATURE.md).

This can be done for a particular folder, by adding a `.github` folder adjacent to the git directory, or organization-wide, by implementing a `.github` repo.

### Pull Request Templates

Within a given repo's `.github` folder, a user can add a `PULL_REQUEST_TEMPLATE.md` file to set a template for future pull requests. This template will automatically be added when users make a pull request.

### Issue Ticket Templates

Within a given repo's `.github` folder, a user can add a `ISSUE_TICKET` folder to create custom issue ticket formats, either in `.yml` or `.md` form. The examples provided within this repository are in markdown form.

To ensure that issues cannot be created without a template, add a `config.yml` file with `blank_issues_enabled: false` as its contents.

For Markdown files, YAML frontmatter with a `name` and `title` field are required.