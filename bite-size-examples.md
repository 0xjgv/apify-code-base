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
[Source.](https://github.com/juansgaitan/act-utils/blob/master/executions-merger.js)
***
