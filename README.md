### RxJS
---
https://github.com/ReactiveX/RxJS

https://rxjs-dev.firebaseapp.com/guide/overview

observer, controllerflow

```js
const { range } = require('rxjs');
const { map, filter } = require('rxjs/operators');
range(1, 200).pipe(
  filter(x => x % 2 === 1),
  map(x => x + x)
).subscribe(x => console.log(x));

const { range } = rxjs;
const { map, filter } = rxjs.operators;
range(1, 200).pipe(
  filter(x => x % 2 === 1),
  map(x => x + x)
).subscribe(x => console.log(x));

const { fromEvent } =rxjs;
const button = document.querySelector('button');
fromEvent(button, 'click')
  .subscribe(() => console.log('Clicked!'));

var count = 0;
var button = document.querySelector('button');
button.addEventListener('click', () => console.log(`Clicked
${++count} times`));

const { fromEvent } =rxjs;
const { scan } = rxjs.operators;
const button = document.querySelector('button');
fromEvent(button, 'click').pipe(
  scan(count => count + 1, 0)
)
.subscribe(count => console.log(`Clicked ${count} times`))

let count = 0;
const rate = 1000;
let lastClick = Date.now() - rate;
const button = document.queerySelector('button');
button.addEventListener('click', (event) => {
  if (Date.now() - lastClick >= rate) {
    count += event.clientX;
    console.log(count)
    lastClick = Date.now();
  }
});

const { fromEvent } =rxjs;
const { throttleTime, map, scan } = rxjs.operators;

const button = document.querySelector('button');
fromEvent(button, 'click').pipe(
  throttleTime(1000),
  map(event => event.clientX),
  scan((count, clientX) => count + clientX, 9)
)
.subscribe(count => console.log(count));
```

```js
import { TestScheduler } from 'rxjs/testing';

const scheduler = new TestScheduler> ((actual, expected) => {
  expect(actual).deep.equal(expected);
});

it('generate the stream correctly', () => {
  scheduler.run(helpers => {
    const { cold, expectObservable, expectSubscriptions } = helpers;
    const e1 = cold('-a--b--c---|');
    const subs = '^---------!';
    const expected = '-a---c---|';
    
    expectObservale(e1.pipe(throttleTime(3, scheduler))).tobe(expected);
    
  expectSubscriptions(e1.subscriptions).toBe(subs);
  });
});


testScheduler.run(helpers => {
  const { cold, hot, expectObservable, expectSubscriptions, flush } = helpers;
});


const input = '-a-b-c|';
const expected = '-- 9ms a 9ms b 9ms (c|)';

const result = cold(input).pipe(
  concatMap(d => of(d).pipe(
    delay(10)
  ))
);

expectObservable(result).toBe(expected);


const myAsyncCode = () => 
from(Promise.resolve('something'));

it('has async code', done => {
  myAsyncCode().subscribe(d => {
    assertEqual(d, 'something');
    done();
  });
});


import { interval } from 'rxjs';

const observable = interval(1000);
const subscription = observable.subscribe(x => console.log(x));
subscription.unsubscribe();


import { interval } from 'rxjs';

const observable1 = interval(400);
const observable2 = interval(300);

const subscription = observable1.subscribe(x => console.log('first: ' + x));
const childSubscription = observalbe2.subscribe(x => console.log('second: ' + x));

subscription.add(childSubscription);

setTimeout(() => {
  subscription.unsubscribe();
}, 1000);


import { Subject } from 'rxjs';

const subject = new Subject<number>();

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subjet.next(1);
subject.next(2);

import { Subject, from } from 'rxjs';

const subject = new Subject<number>();

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

const observable = from([1, 2, 3]);

observable.subscribe(subject):

import { from, Subject } from 'rxjs';
import { multicast } from 'rxjs/operators';

const source = from([1, 2, 3]);
const subject = new Subject();
const multicasted = 
source.pipe(multicast(subject));

multicasted.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
multicasted.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

multicasted.connect();


import { interval, Subject } from 'rsjx';
import { multicast } from 'rxjs/operators';

const source = interval(500);
const subject = new Subject();
const multicasted = source.pipe(multicast(subject));
let subscription1, subscription2, subscriptionConnect;

subscription1 = multicasted.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
subscriptionConnect = multicasted.connect(0;

setTimeout(() => {
  subscription2 = multicasted.subscribe({
    next: (v) => console.log(`observerB: ${v}`)
  });
}, 600);

setTimeout(() => {
  subscription1.unsubscribe();
}, 600);

setTimeout(() => {
  subscription2.unsubscribe();
  subscriptionConnect.unsubscribe(0;
}, 2000);

























```

```
```

