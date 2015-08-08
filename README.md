# `combineLatestObj` for RxJS

`npm install rx-combine-latest-obj`

## Usage

Given these observables:
```js
const a$ = Rx.Observable.interval(50).take(3);
const b$ = Rx.Observable.just('Boston');
const c$ = Rx.Observable.just('Colorado');
```

Make an observable which is the combination of them, bundled as an object.

```js
import combineLatestObj from 'rx-combine-latest-obj';

const state$ = combineLatestObj({a$, b$, c$});
// or const state$ = combineLatestObj({a: a$, b: b$, c: c$});

state$.subscribe(x => console.dir(x));
// {a: 0, b: 'Boston', c: 'Colorado'}
// {a: 1, b: 'Boston', c: 'Colorado'}
// {a: 2, b: 'Boston', c: 'Colorado'}
```

It takes [Cycle.js' hungarian notation `$`](http://cycle.js.org/basic-examples.html#what-does-the-suffixed-dollar-sign-mean) into consideration, returning an object whose's keys don't have the $.

The above is more convenient than writing:
```js
var stateAlt$ = Rx.Observable.combineLatest(
  a$, b$, c$, (a, b, c) => ({a, b, c})
);
```
