# Header generator
NodeJs package for generating browser-like headers.

<!-- toc -->

- [Installation](#installation)
- [Usage](#usage)
- [Examples](#examples)
- [API Reference](#api-reference)

<!-- tocstop -->

## Installation
Add this repository as an npm dependency and run the npm install command. No further setup is needed after that.
## Usage
To use the generator, you need to create an instance of the HeaderGenerator class which is exported from this package. Constructor of this class accepts a HeaderGeneratorOptions object, which can be used to globally specify what kind of headers you are looking for: 
```js
const HeaderGenerator = require('header-generator');
let headerGenerator = new HeaderGenerator({
        browsers: [
            {name: "firefox", minVersion: 80},
            {name: "chrome", minVersion: 87},
        ],
        devices: [
            "desktop"
        ],
        operatingSystems: [
            "windows"
        ]
});
```
You can then get the headers using the getHeaders method, either with no argument, or with another HeaderGeneratorOptions object, this time specifying the options only for this call (overwriting the global options when in conflict) and using the global options specified beforehands for the unspecified options:
```js
let headers = headersGenerator.getHeaders({
        operatingSystems: [
            "linux"
        ],
        locales: ["en-US", "en"]
});
```
This method always generates a random realistic set of headers, excluding the request dependant headers, which need to be filled in afterwards. Since the generation is randomized, multiple calls to this method with the same parameters can generate multiple different outputs.
## Examples
A result that can be generated for the usage example above:
```json
{
    "one": 2,
    "three": {
        "point_1": "point_2",
        "point_3": 3.4
    },
    "list": [
        "one",
        "two",
        "three"
    ]
}
```
## API Reference
All public classes, methods and their parameters can be inspected in this API reference.

<a name="HeaderGenerator"></a>

### HeaderGenerator
HeaderGenerator randomly generates realistic browser headers based on specified options.


* [HeaderGenerator](#HeaderGenerator)
    * [`new HeaderGenerator(options)`](#new_HeaderGenerator_new)
    * [`.getHeaders(options)`](#HeaderGenerator+getHeaders)


* * *

<a name="new_HeaderGenerator_new"></a>

#### `new HeaderGenerator(options)`

| Param | Type | Description |
| --- | --- | --- |
| options | [<code>HeaderGeneratorOptions</code>](#HeaderGeneratorOptions) | default header generation options used unless overridden |


* * *

<a name="HeaderGenerator+getHeaders"></a>

#### `headerGenerator.getHeaders(options)`
Generates a single set of headers using a combination of the default options specified in the constructor
and their possible overrides provided here.


| Param | Type | Description |
| --- | --- | --- |
| options | [<code>HeaderGeneratorOptions</code>](#HeaderGeneratorOptions) | specifies options that should be overridden for this one call |


* * *

<a name="Browser"></a>

### `Browser`

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | One of "chrome", "firefox", "safari" for now. |
| minVersion | <code>number</code> | Minimal version of browser used. |
| maxVersion | <code>number</code> | Maximal version of browser used. |
| httpVersion | <code>string</code> | Either 1 or 2. If none specified the global `httpVersion` is used. |


* * *

<a name="HeaderGeneratorOptions"></a>

### `HeaderGeneratorOptions`

| Param | Type | Description |
| --- | --- | --- |
| browsers | [<code>Array.&lt;Browser&gt;</code>](#Browser) | List of Browsers to generate the headers for. |
| operatingSystems | <code>Array.&lt;string&gt;</code> | List of operating systems the headers for.  “windows” “macos” “linux” “android” “ios”. We don't need more I guess. |
| browserList | <code>Array.&lt;string&gt;</code> | Browser definition based on the https://www.npmjs.com/package/browserslist. |
| devices | <code>Array.&lt;string&gt;</code> | List of devices to generate the headers for. One of "desktop", "mobile". |
| locales | <code>Array.&lt;string&gt;</code> | List of at most 10 languages to include in the `Accept-Language` request header. |
| httpVersion | <code>string</code> | Http version to be used to generate headers. http 1 and http 2 sends different header sets. |
| strategies | <code>string</code> | Strategies for generating headers - used for simplifying the configuration. For example: "modern-browsers". |


* * *

