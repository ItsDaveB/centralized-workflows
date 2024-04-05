# Lighthouse CI Workflow Documentation

## Overview
The **Lighthouse CI** reusable workflow integrates Google's Lighthouse performance and SEO auditing tool into your GitHub Actions, allowing automated running of Lighthouse audits on your projects. This reusable workflow streamlines performance checks, ensuring that your website maintains high standards for speed, accessibility, and SEO.  The results are outputted to the Job summary as markdown, and also uploaded as an artifact so you can access the full audit.

## Job Summary Preview
![image](https://github.com/dpbeaumont/centralized-workflows/assets/49551821/5f13183a-99fc-4482-a85a-188c07f4f16d)

## Full Audit Report Artifact Preview
![image](https://github.com/dpbeaumont/centralized-workflows/assets/49551821/c991bec2-6c44-4f62-bf97-6a16b9df14dc)

## Inputs
The workflow accepts several inputs to customize the Lighthouse audit according to your project needs:

### `lighthouserc-path`
- **Description**: Path to `lighthouserc.yml`.
- **Required**: Yes.
- **Type**: String.

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

## Jobs
The workflow contains a job named `lighthouse-ci-audit`, which executes the following steps:

1. **Checkout**: Checks out your repository.
2. **Set up Node.js**: Sets up the Node.js environment based on the specified node version.
3. **Install dependencies**: Installs the project's dependencies using `yarn install`.
4. **Build Project**: Runs the build process for your project based on the provided build command.
5. **Run Lighthouse CI**: Installs the Lighthouse CLI and executes the audit as per the configuration in `lighthouserc.yml`.
6. **Archive Lighthouse Results**: Uploads the Lighthouse audit results as an artifact, available for download if the audit is successful.
7. **Add Markdown To Job Summary**: Runs a custom script, that expects markdown to be returned, this then adds it to the job summary. This requires a script path to be provided in `results-summary-script`.

## `lighthouserc.yml` Configuration Example

The `lighthouserc.yml` file configures the Lighthouse CI workflow and allows configuration to be applied to the audit. Below is an example of this configuration file that you can use as a starting point for your project:

```yaml
ci:
  collect:
    numberOfRuns: 2
    startServerCommand: yarn start
    url:
      - http://localhost:3000
  assert:
    includePassedAssertions: true
    assertions:
      "categories:performance":
        - warn
        - minScore: 1.0
      "categories:accessibility":
        - warn
        - minScore: 0.99
      "categories:best-practices":
        - warn
        - minScore: 0.95
      "categories:seo":
        - warn
        - minScore: 1.0
  upload:
    target: filesystem
    outputDir: ./lighthouseci
  settings:
    chromeFlags:
      - --ignore-certificate-errors
    preset: desktop
    onlyCategories:
      - performance
      - accessibility
      - best-practices
      - seo
```

## Further Configuration and Advanced Options

For a deeper understanding and more advanced configuration options of the `lighthouserc.yml` file, you can refer to the official Lighthouse CI documentation. This resource provides in-depth information on a wide range of settings and customization options that you can leverage to tailor the Lighthouse CI workflow to your project's specific needs.

Access the complete Lighthouse CI configuration documentation here: [Lighthouse CI Configuration](https://github.com/GoogleChrome/lighthouse-ci/blob/main/docs/configuration.md).
