# reactive-x

http://reactivex.io/
https://www.pluralsight.com/

user: my-umpqua-email
password: namae

## day one

Observable
Subject

concatAll (arrays) reduces by one dimension

you will write code in two parts
* building the collection you want
* consuming the data in that collection and doing something with it

they is no difference between events and arrays (events and arrays are both collections)

* with the **iterator** pattern you pull items out (until error or it's done)
* with the **observer** pattern you push items out 

observable === collection + time

observable can model
* events
* async server requests
* animations

var mouseMoves = Observable.fromEvent(element, 'mousemove');

// subscribe
var subscription = mouseMoves.forEach(console.log)

// unsubsribe
subscription.dispose()

// subscribe
var subscription = mouseMoves.forEach (
  // next data
  event => console.log(event)
  // error
  error => console.log(error)
  // completed
  () => console.log('done')
)

hot observable
cold observable

concatAll is observable of observables

takeUntil source collection, stop collection until the second collection pushes anything

DON'T unsubscribe from events

## day two

mergeAll
concatAll
switchLatest
tableUntil

understand the differences between inner and outer observables

we are going to write declarative code (verses imperative code)

>Declarative programming is a programming paradigm … that expresses the logic of a computation without describing its control flow.

>Imperative programming is a programming paradigm that uses statements that change a program’s state.

When we start solving these probems we are going to describe them in four steps
1. what collections (observables) do I have
2. what collection (observable) do I want
3. how do I get from the collections I have to the collection I want
4. what am I going to do with the data that comes out of it

```javascript
// netflix search

// this builds the collections we want
var searchResultSets =
  keyPresses
    .throttle(250)
    .map(key => getJSON('/searchResults?q=' + input value)
      .retry(3))
    .switchLatest();

// this part consumes the data and put it on the screen
searchResultsSets.forEach(
    resultsSet => updateSearchResults(resultSet),
    error => showMessage('the server is down';)
)
```

**throttle** reduces the number of network requests
**map** in this case map is returning another collection - taking a one dimensional collection and returning a two dimensional collection 
**retry** is on the observable type
**switchLatest** select the right flatting pattern (operator) before we do a **forEach** operates on lazy observables

sometimes you need concatAll() and concatAll to flatten a three dimensional to a one dimensional

catch(e => Observable.empty) - catch takes a function and the function can optionally return an observable to resume from

Promises are not very useful for most of the problems we encounter in user
interface design. Promises cannot be cancelled.

http://jhusain.github.io/learnrx/

NOTE: detail all event in the net feature flag code and detail whether they complete or run forever. Do the http requests complete

https://www.youtube.com/watch?v=PhggNGsSQyg

