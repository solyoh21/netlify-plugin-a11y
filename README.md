# netlify-plugin-a11y

Run your critical pages through [pa11y](https://github.com/pa11y/pa11y) and fail build if accessibility failures are found.

> NOTICE: This is an experimental feature. Subject to lots of change.

## Demo

https://netlify-plugin-a11y.netlify.com/

## Overview

Run axe-cli and fail build if accessibility failures are found.

## Demonstration

See this plugin being used in this simplified demo site:

You can switch to `resultMode = "warn"` so that builds don't fail:

![image](https://user-images.githubusercontent.com/6764957/77146484-868d4a80-6a61-11ea-84cc-703c2abd6d6e.png)

## Usage

### Prerequisites

- npm and node
- @Netlify/build (later this will be included in the Netlify CLI)
- A free [Netlify account](https://netlify.com)
- Opt-in to Netlify Build Plugin feature support (Not yet publicly available, sorry)


### Including this plugin in a project

This plugin can be included via npm. Install it as a dependency for your project like so:

```
npm install --save netlify-plugin-axe
```

### Configuration

This plugin will fetch the specified feeds and stash their data prior to the execution of the `build` command you have specified in your Netlify configuration. The desired feeds can be specified in the `netlify.toml` config file. For simpler configuration syntax, I recommend using yaml rather than toml by instead including a `netlify.yml` file.

To use plugins, a `plugins` array should be specified in your `netlify.yml`. Each plugin can then be specified with its parameters like so:

```yaml
plugins:
  - netlify-plugin-axe:
    # type: ./path-to-plugin-file | npm-module-name
    type: netlify-plugin-fetch-feeds
    config:
      site: mycoolsite.netlify.com # your Netlify site url
      # https://github.com/dequelabs/axe-cli#running-specific-rules
      axeFlags: --tags wcag2a
```


### Execution in Netlify

Once installed and configured, the plugin will automatically run in the Netlify CI during its specified Netlify Build lifecycle event.

### Executing locally

To test the execution of the Netlify Build lifecycle locally, first ensure that netlify-build is installed:

```bash
# Ensure that you have the netlify build command available
# (in future this will be provided via the CLI)
npm install @netlify/build -g

# In the project working directory, run the build as netlify would with the build bot
netlify-build
```


## Issues

- https://github.com/jaimeiniesta/serverless-axe-cli/pull/1
- https://github.com/adieuadieu/serverless-chrome/issues/143
- https://gist.github.com/stephenmathieson/57c1fa4a8a6bdbb489f91d4a4f713ee9
- npm install chromedriver
  - https://github.com/SeleniumHQ/selenium/issues/4863
  - https://www.selenium.dev/documentation/en/webdriver/driver_requirements/
- https://github.com/dequelabs/axe-cli/issues/84