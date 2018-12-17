
# Puppeteer Chromium Resolver

![npm](https://img.shields.io/npm/v/puppeteer-chromium-resolver.svg)
![npm](https://img.shields.io/npm/dt/puppeteer-chromium-resolver.svg)
![David](https://img.shields.io/david/cenfun/puppeteer-chromium-resolver.svg)

* A tool to customize [puppeteer](https://github.com/GoogleChrome/puppeteer)
* Detect chromium from local path.
* Download chromium from custom/mirror host.
* Cache chromium to local.
* Try to launch chromium and returns launchable property
* Returns puppeteer and executablePath

## Install 
```sh
npm install puppeteer-chromium-resolver --save
```
## Usage
```js

var puppeteerResolver = require("puppeteer-chromium-resolver");
var revisionInfo = await puppeteerResolver({
    revision: "",
    detectionPath: "",
    folderName: '.chromium-browser-snapshots',
    hosts: ["https://storage.googleapis.com", "https://npm.taobao.org/mirrors"],
    retry: 3
});

console.log("Chromium revision installed and launchable is " + revisionInfo.launchable);

var browser = await revisionInfo.puppeteer.launch({
    headless: true,
    args: ['--no-sandbox'],
    executablePath: revisionInfo.executablePath
}).catch(function (error) {
    console.log(error);
});

var page = await browser.newPage();
await page.goto('https://www.google.com');
await browser.close();

```
