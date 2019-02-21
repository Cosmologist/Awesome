# Promise
В параллельных вычислениях это подход для извещения о завершении обработки (успешной или нет) и получения результата. ```computeAsync().then(successComputationCallback, failComputationCallback)```.
 
## Example
```js
function computeAsync(inputData) {
  return new Promise(function (resolve, reject) {
    ... // долгие вычисления
    
    if (error) {
      // уведомляем что вычисления завершены с ошибкой
      // можем передать любые данные, которые будут переданы в failComputationCallback (смотри ниже)
      reject(errorData)
    } else {
      // уведомляем что вычисления завершены с ошибкой
      // можем передать любые данные, которые будут переданы в successComputationCallback (смотри ниже)
      resolve(data) // уведомляем что вычисления завершены успешно, можем вернуть дополнительную информацию
    }
  }
)
...
computeAsync().then(successComputationCallback, failComputationCallback)
```
## Links
- [Using_promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
