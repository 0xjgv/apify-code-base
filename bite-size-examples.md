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
__Keywords:__ _async, promise, good practice, use-case, sequence, reduce._
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
__Keywords:__ _good practice, use-case, input, error handling, ._
[Source example.](https://github.com/jancurn/act-analyse-pages/blob/master/main.js)
