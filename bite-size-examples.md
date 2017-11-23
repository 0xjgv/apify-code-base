## Immutable sequence of promise/s requests.

```javascript
/**
* @arg Array items
* @arg Async Function asyncFunction
* @return [Promise]
*/
function getInSequence(items, asyncFunction) {
  return items.reduce((previous, item) => (
  previous.then(accumulator => (
  asyncFunction(item).then(result => accumulator.concat(result))
  ))
  ), Promise.resolve([]));
}
```
__Keywords:__ _async, promise, best practice, use-case, sequence, reduce._
[Source example.](https://github.com/juansgaitan/act-utils/blob/master/executions-merger.js)
***

## Check the INPUT_TYPE
We have used ```type-check``` in this example, though any type checking library or self written check would do the trick.
```javascript
const { typeCheck } = require('type-check');

const INPUT_TYPE = `{
  urls: [String],
  urlToTextFileWithUrls: Maybe String,
  concurrency: Maybe Number,
  storePagesInterval: Maybe Number,
  screenshotWidth: Maybe Number,
  screenshotHeight: Maybe Number
}`;

const input = await Apify.getValue('INPUT');
if (!typeCheck(INPUT_TYPE, input)) {
  console.error('Expected input:');
  console.error(INPUT_TYPE);
  console.error('Received input:');
  console.error(util.inspect(input));
  throw new Error('Received invalid input');
}
```
__Keywords:__ best practice, use-case, input, error handling._
[Source example.](https://github.com/jancurn/act-analyse-pages/blob/master/main.js)
***

## Apify's built in methods

All the methods allow the programmer to ```call``` another **Act**, ```getValue```, ```setValue```, with **no** previous _client set-up or auth_.
```javascript
const Apify = {
  main,
  getEnv,
  getValue,
  setValue,
  call,
  readyFreddy,
  setPromisesDependency,
  getPromisesDependency,
  browse,
  launchWebDriver,
  launchPuppeteer,
  client: apifyClient,
  events: new EventEmitter(),
};
```
__Keywords:__ _use-case, methods, api, best practice._

[Official Documentation.](https://www.apify.com/docs/sdk/apify-runtime-js/latest#module-Apify-client)
[Source.](https://github.com/Apifier/apify-runtime-js/blob/master/src/index.js)
***
