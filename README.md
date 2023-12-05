# puppeteer-har

Generate HAR file with [puppeteer](https://github.com/GoogleChrome/puppeteer).

## Note about this fork

This repository is a fork of another fork of the initial puppeteer-har package.
Main changes:
- Remove npm package release configurations (`husky`, `pinst`, `semantic-release`,
  etc.) to install library from GitHub link
- `.devcontainer/` configurations for [development with
  VScode](https://gist.github.com/yohhaan/b492e165b77a84d9f8299038d21ae2c9)
- Dependencies upgraded and fix type issues

## Install

```
yarn add https://github.com/yohhaan/puppeteer-har
```

## Usage

```es6
import puppeteer from "puppeteer"
import { captureNetwork } from "puppeteer-har"

const browser = await puppeteer.launch()
const page = await browser.newPage()

const getHar = await captureNetwork(page)

await page.goto("http://example.com")

const har = await getHar()
await browser.close()
```

## `captureNetwork(page[, options])`

Start capturing the network traffic of the given puppeteer page.

### Returns

`captureHar` returns a method that will stop capturing traffic and return a HAR file when called.

### `options`

#### `saveResponses`

Defaults to `false`.
If set the HAR file will also include the responses to network requests.

#### `captureMimeTypes`

Defaults to `['text/html', 'application/json']`.
When responses should be saved you can specify which response types to include through this array.
