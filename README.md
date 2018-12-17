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
```

```
```

```
```

