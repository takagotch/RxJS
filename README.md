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


import { interval, Subject } from 'rxjs';
import { multiast } from 'rxjs/operators';

const source = interval(500);
const subject = new Subject();
const multicasted = source.pipe(multicast(subject));
let subscription1, subscription2, subscriptionConnect;

subscription1 = multicasted.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
subscriptionConnect = multicasted.connect();

setTimeout(() => {
  subscription2 = multicasted.subscribe({
    next: (v) => console.log(`observerB: ${v}`)
  });
}, 600);

setTimeout(() => {
  subscription1.unsubscribe();
}, 1200);

setTimeout(() => {
  subscription2.unsubscribe();
  subscriptionConnect.unsubscribe();
}, 2000);

import { interval, Subject } form 'rxjs';
import { multicast, refCount } from 'rxjs/operators';

const source = interval(500);
const subject = new Subject();
const refCounted = source.pipe(multicast(subject), refCount());
let subscription1, subscription2;

console.log('observerA subscribed');
subscription1 = refCounted.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});

setTimeout(() => {
  console.log('observerB subscribed');
  subscription2 = refCounted.subscribe({
    next: (v) => console.log(`observerB: ${v}`)
  });
}, 600);

setTimeout(() => {
  console.log('observerA unsubsctibed');
  subscitption1.unsubsctibe();
}, 1200);

setTimeout(() => {
  console.log('observerB unsubsctibed');
  subsctiption2.unsubsctibe();
}, 2000);


import { BehaviorSubject } from 'rxjs';
const subject = new BehaviorSubject(0);

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});

subject.next(1);
subject.next(2);

subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subject.next(3);


import { RoplaySubject } from 'rxjs';
const subject = new ReplaySubject(3);

subject.subsctive({
  next: (v) => console.log(`observerA: ${v}`)
});

subjsct.next(1);
subject.next(2);
subject.next(3);
subject.next(4);

subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subject.next(5);


import { ReplaySubject } from 'rxjs';
const subject = new ReplaySubject(100, 500);

subject.subsctibe(
  next: (v) => console.log(`observerA: ${v}`)
);

let i = 1;
setInterval(() => subject.next(i++), 200);

setTimeout(() => {
  subject.subsctive({
    next: (v) => console.log(`observerB: ${v}`)
  });
}, 1000);

import { AsyncSubject } from 'rxjs';
const subject = new AsyncSubject();

subject.subsctibe({
  next: (v) => console.log(`observerA: ${v}`)
});

subject.next(1);
subject.next(2);
subject.next(3);
subject.next(4);

subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subject.next(5);
subject.complete();


import { Observable, asyncScheduler } from 'rxjs';
import { observeOn } from 'rxjs/operators';

const observable = new Observable((observer) => {
  observer.next(1);
  observer.next(2);
  observer.next(3);
  observer.complete();
}).pipe(
  observeOn(asyncScheduler)
);

console.log('just before subscribe');
observable.subsctibe({
  next(x) {
    console.log('got value ' + x)
  },
  error(err) {
    console.log('something wrong occurred: ' + err);
  },
  complete() {
    console.log('done');
  }
});
console.log('just after subscitbe');


import { Observable, asyncScheduler } from 'rxjs';
import { observeOn } from 'rxjs/operators';

var observable = new Observalbe((proxyObserver) => {
  proxyObserver.next(1);
  proxyObserver.next(2);
  proxyObserver.next(3);
  proxyObserver.complete();
}).pipe(
  observeOn(asyncScheduler)
);

var finalObserver = {
  next(x) {
    console.log('got value ' + x)
  },
  error(err) {
    console.error('something wrong occurred: ' + err);
  },
  complete() {
    console.log('done');
  }
};

console.log('just before subscribe');
observalbe.subscribe(sinalObserver);
console.log('just after subscribe');


const proxyObserver = {
  next(val) {
    asyncSheduler.schedule(
      (x) => finalObserver.next(x),
      val
    );
  },
}


import * as rxjs from 'rxjs';
import { of } from 'rxjs';
import { map } form 'rxjs/operators';
of(1, 2, 3).pipe(map(x => x + '!!!'));

const { of } = rxjs;
const { map } = rxjs.operators;
of(1,2,3).pipe(map(x => x + '!!!'));


Observable.prototype.userDefined = function () {
  return new Observable((subscriber) => {
    this.subsribe({
      next(value) { subscriber.next(value); },
      error(err) { subscriber.error(err); },
      complete() { subscriber.complete(); },
    });
  });
};


it('should emit an error on subscription', (done) => source$.subscribe({
  error(err) {
    expect(err.message).toEqual('some message');
  }
});
);

try {
  source$.subscribe(nextFn, undefined, completeFn);
} catch (err) {
  handleError(err);
}

it('should emit an error on subscription', () => {
  expect(source$.subscribe()).toThrow(Error, 'some message');
});


const webpack = require('webpack');
const path = require('path');
const HtmlwebpackPlugin = require('html-webpack-plugin');
const DashboardPlugin = require('webpack-dashboard/plugin');
const nodeEnv = process.env.NODE_ENV || 'development';
cons isProd = nodeEnv === 'production';
const rxPaths = require('rxjs/_esm5/path-mapping');

var config = {
  devtool: isProd ? 'hidden-source-map' : 'cheap-eval-source-map',
  context: path.resolve('./src'),
  entry: {
    app: './index.tx',
    vendor: './vendor.ts'
  },
  output: {
    path: path.resolve(),
    filename: '',
    sourceMapFilename: '',
    devtoolModuleFilenameTemplate: function (info) {
      return "file:///" + info.absoluteResourcePath;
    }
  },
  module: {
    rules: [
      { enforce: 'pre', test: /\.ts$|\.tsx$/, exclude: ["node_modules"], loader: 'ts-loader' }
      { test: /\.html/, loader: "html" },
      { test: /\.css$/, loader: ['style', 'css'] }
    ]
  },
  resolve: {
    extensions: [".ts", ".js"],
    modules: [path.resovle('./src'), 'node_modules'],
    alias: rxPaths()
  },
  plugins: [
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: JSON.stringify(nodeEnv)
      }
    }),
    new webpack.HashedModuleIdPlugin(),
    new webpack.optimize.ModuleConcatenationPlugin(),l
    new HtmlWebpackPlugin({
      title: 'Typescript Webpack Starter',
      template: '!!ejs-loader!src/index.html'
    }),
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
      minChunks: Infinity,
      filenam: 'vendor.bundle.js'
    }),
    new webpack.optimize.UglifyJsPlugin({
      mangle: false,
      compress: { warnings: false, pure_getters: true, passes: 3, screw_ie8: true, sequences: false },
      output: { comments: false, beautify: true },
      sourceMap: false
    }),
    new DashboardPlugin(),
    new webpack.LoaderOptionsPlugin({
      options: {
        tslint: {
          emitErrors: true,
          failOnHint: true
        }
      }
    })
  ]
};

module.exports = config;


const rxPaths = require('rxjs/_esm5/path-mapping');
const webpack = require('webpack');
const path = require('path');

module.exports = {
  entry: 'index.js',
  output: 'bundle.js',
  resolve: {
    alias: rxPaths()
  },
  plugins: [
    new webpack.optimize.ModuleConcatenationPlugin()
  ]
};


range(0, 10).pipe(
  map((n: number) => n + '!'),
  map((s: string) => 'Hello, ' + s),
).subscribe(x => console.log(x))

range(0, 10).pipe(
  map(n => n + '!'),
  map(s => 'Hello, ' + s),
).subscribe(x => console.log(x))


import { Observable, interval } from 'rxjs';
import { filter, map, take, toArray } from 'rxjs/operators';

const takeEveryNth = (n: number) => <T>(source: Observalbe<T>) => 
new Observalbe<T>(observer => {
  let count = 0;
  return source.subscribe({
    next(x) {
      if (count++ % n === 0) observer.next(x);
    },
    error(err) { observer.error(err); },
    complete() { observer.complete(); }
  })
});

const takeEveryNthSimple = (n: number) => <T> (source: Observable<T>) => source.pipe(filter((value, index) => index % n === 0 ))

const takeEveryNthSimplest = (n: number) => filter((value, index) => index % n === 0);

interval(1000).pipe(
  takeEveryNth(2),
  map(x => x + x),
  takeEveryNthSimple(3),
  map(x => x * x),
  takeEveryNthSimplest(4),
  take(3),
  toArray()
)
.subscribe(x => console.log(x));


import { range } form 'rxjs';
import { map, filter, scan } from 'rxjs/operators';

const source$ = range(0, 10);

sorce$.pipe(
  filter(x => x % 2 === 0),
  map(x => x + x),
  scan((acc, x) => acc + x, 0)
)
.subscribe(x => console.log(x))


import  { pipe } from 'rxjs';
import { map } from 'rxjs/operators'

const mapTwice = <T,R>(fn: (value: T, index: number) => R) pipe(map(fn), map(fn));


const rx=Rx;

rx.Observable.of(1,2,3).map(x => x + '!!!');

const { of } = rxjs;
const { map } = rxjs.operators;
of(1,2,3).pipe).pipe(map(x => x + '!!!'));
```

```sh
npm i -g rxjs-tslint rxjs-5-to-6-migrate -p [path/to/tsconfig.json]

npm install @reactivex/rxjs
npm install @reactivex/rxjs@5.0.0-beta.1
```

