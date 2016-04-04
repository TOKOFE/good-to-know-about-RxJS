### How to chain Observables

When we use `Promises` sometimes we chain promise in the `then` method by returning prmises. It makes our code clean and readable.

```
httpService.post(url, data, options)
  .map(response => response.json())
  .toPromise()
  .then((response: any) => {
    // do something
    return httpService.get(url).toPromise(); // return promise to chain it
  })
  .then((response: any) => {
    // do something
  })
  .catch();
```

Let's make it work in Observables. You can implement it with `switchMap` or `flatMap` operators. 
They transform the items emitted by an Observable into Observables so that you can chain observables. We can change the above code with `switchMap`.

```
httpService.post(url, data, options)
  .switchMap((response: any) => {
    let res = response.json();
    
    // do something
    
    return httpService.get(url);
  })
  .toPromise() // you can use map or subscribe instead of converting to `Promise`
  .then()
  .catch();
```

#### More resources

* [Using `switchMap`](http://stackoverflow.com/questions/26935821/rxjava-chaining-observables)
* [Using `flapMap`](http://stackoverflow.com/questions/26959011/how-to-chain-asynchronous-operations-using-java-rx-observable)
* [FlatMap](http://reactivex.io/documentation/operators/flatmap.html)
