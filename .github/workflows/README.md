# Lighthouse CI Workflow Documentation

## Overview
The **Lighthouse CI** workflow integrates Google's Lighthouse performance and SEO auditing tool into your GitHub Actions, allowing automated running of Lighthouse audits on your projects. This reusable workflow streamlines performance checks, ensuring that your website maintains high standards for speed, accessibility, and SEO.

## Inputs
The workflow accepts several inputs to customize the Lighthouse audit according to your project needs:

### `working-directory`
- **Description**: Working Directory for the Lighthouse Audit.
- **Required**: No.
- **Default**: `"."` (current directory).
- **Type**: String.

### `node-version`
- **Description**: Node.js Version.
- **Required**: No.
- **Default**: `"14.x || 16.x || 18.x"`.
- **Type**: String.

### `lhci-version`
- **Description**: Lighthouse CLI Version.
- **Required**: No.
- **Default**: `"0.13.x"`.
- **Type**: String.

### `lighthouserc-path`
- **Description**: Path to `lighthouserc.yml`.
- **Required**: Yes.
- **Type**: String.

## Jobs
The workflow contains a job named `lighthouse-ci-audit`, which executes the following steps:

1. **Checkout**: Checks out your repository.
2. **Set up Node.js**: Sets up the Node.js environment based on the specified node version.
3. **Install dependencies**: Installs the project's dependencies using `yarn install`.
4. **Build Project**: Runs the build process for your project based on the provided build command.
5. **Run Lighthouse CI**: Installs the Lighthouse CLI and executes the audit as per the configuration in `lighthouserc.yml`.
6. **Archive Lighthouse Results**: Uploads the Lighthouse audit results as an artifact, available for download if the audit is successful.
7. **Convert JSON to Markdown and Add to Job Summary**: Converts the Lighthouse audit results from JSON to Markdown and appends them to the job summary. This requires a script path to be provided in `results-summary-script`.

## Integration
To integrate this workflow into your project:

- Define the workflow in a `.yml` file within the `.github/workflows` directory of your repository.
- Customize the inputs as needed, ensuring that `lighthouserc-path` is correctly specified.
- Trigger the workflow as part of your CI process to automatically run Lighthouse audits.

This workflow facilitates continuous performance and SEO checks, keeping your web project optimized and up to standards.

## Further Configuration and Advanced Options

For a deeper understanding and more advanced configuration options of the `lighthouserc.yml` file, we recommend referring to the official Lighthouse CI documentation. This resource provides in-depth information on a wide range of settings and customization options that you can leverage to tailor the Lighthouse CI workflow to your project's specific needs.

Access the complete Lighthouse CI configuration documentation here: [Lighthouse CI Configuration](https://github.com/GoogleChrome/lighthouse-ci/blob/main/docs/configuration.md).