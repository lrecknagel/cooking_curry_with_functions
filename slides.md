---
theme: ./theme
fonts:
  sans: 'Dank Mono'
  serif: 'Dank Mono'
  mono: 'Dank Mono'
  local: 'Dank Mono'
colorSchema: dark
highlighter: shiki
lineNumbers: true
layout: intro
title: cooking => curry => with => functions
---

# cooking => curry => with => functions

Some recipes for functional programming

<div class="absolute bottom-10">
  <span class="rounded cursor-pointer hover:bg-white hover:bg-opacity-10">
    Klimaneutrale Immobilien.<br/>
    Einfach. Profitabel. Jetzt.
  </span>
</div>
<div class="absolute bottom-10 right-10">
  <img src="/ae_logo_white.png" class="w-30"/>
</div>

<style>
h1 {
  font-size: 3rem !important;
}
</style>

---
layout: fact
---

# FP is hard?
its not easy as well as OO isnt!

<!--
OO: generics, polymorphism, solid, inheritance, ...
FP: core concepts
-->

---
layout: fact
---

# about FP
paradigm, functions, math

<!--
Explain the concepts
Show few examples to understand the concepts
note the most interesting parts for a followUp
-->

---
layout: default
---

# Core principles?

- 🧩 **Paradigm** - one major coding paradigm
- 🆎 **Types** - Types != Classes, f-DDD & more
- 🗄️ **Params** - 1st class concept of parameters
- 💿 **Data** - Immutability
- ⚙️ **Functions** - Functions as any, Composition, …
- 💎 **Pureness** - NO?! SideEffects
- 🦄 **Fantasyland** - Monads, Maps, Monoids, Kleislis, …

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
li {
  font-family: 'Dank Mono'
}
</style>

<!--
Standalone - not bound to classes
funcs do the stuff - all is centered around them
-->

---
layout: default
---

# Core principles?

- 🧩 **Paradigm** - one major coding paradigm
- 🆎 **Types** - Types != Classes, f-DDD & more
- 🗄️ **Params** - 1st class concept of parameters
- 💿 **Data** - Immutability
- ⚙️ **Functions** - Functions as any, Composition, …
- 💎 ~~Pureness - NO?! SideEffects~~
- 🦄 ~~Fantasyland - Parameters, Monads, Maps, Monoids, Kleislis, …~~
- ✍🏼 **Examples** - Unarity, PartialApplication, Pureness & Curry

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
li {
  font-family: 'Dank Mono'
}
</style>

<!--
instead of a little of all
we keep some with examples

* pure: fn with same params deliver always same result
* impure: IO, modify data outside of themselfs
* keeping impureness on edges of your composition

fantasyland - all around category theorie, the real basics
-->

---
layout: default
---

# 🆎 Types

* not classes, no inheritance
* set of things
* pure data
* types - types composition
* total
* [Functional DDD](https://fsharpforfunandprofit.com/ddd/)

<br>

```ts {all|1-3|5-10|all}
// totality
int => int        // with throw is not total
int => option int // is total

type HPSubType = Air | Ground
type Power = int
type HP {
  subType: HPSubType
  power: Power
}
```

<!--
basic idea - more on function DDD -> complete own topic
Algebraic / Composable type system
-->

---
layout: fact
---

# 🗄️ Parameterize
decouple behaviour and data

<!--
fn x() => print "1"
fn x(action, data) => action data
-->


---
layout: fact
---

# 💿 Data
immutability, structures, lenses & optics

<!--
structures, lenses & optics -> later
-->

---
layout: fact
---

# ⚙️ functions
functions, functions, functions …

---
layout: default
---

# ⚙️ functions as …

```js {all|1-3|5-7|2,9-12|all}
// as output: any … any -> fn … fn | HigherOrderFunctions
const times2 = x => x * 2
times2(5) // 10

// as inputs: fn … fn -> any … any | Lifting
const unary = fn => arg => fn(arg)
['1','2','3'].map(parseInt) vs. ['1','2','3'].map(unary(parseInt))

// as parameter
const transformListBy = transformerFn => list => list.map(transformerFn);
const times2ForLists = transformListBy(times2);
times2ForLists([1,2,3]) // [ 2, 4, 6 ]
```

<!--
Monadic Binds -> how combine missmatched functions 
  two-track approach
  fn with 1-in & two out to 2-in-out
  fn input, parameter, output
-->

---
layout: default
---

# ⚙️ function composition

```js {all}
const fn1 = A => B
const fn2 = B => C
const fn3 = compose(fn1, fn2) // A => C
```

* operations
* operations composed into services
* services composed into usecases
* … and so on
* & only works with unary functions :(

<!--
encapsulation
-->

---
layout: fact
---

# "basics" ✅
lets see some patterns …

---

# ✍🏼 Immutability & fns as parameters

* reducing / folding data with functions
* apply action on a list-like and accumulate a initial value

<br>

```js{all|1-4|6|7|all}
let res = [];
for (let i = 0; i < [1,2,3]; i++) { 
  res[i] = i - 1
}

const res = [1,2,3].map(_ => _ - 1);
const res = [1,2,3].reduce((currentValue, _) => [...currentValue, _ - 1], []);
// filter ...
```

<!--
immutability -> no loops
common-code, values and actions
-->

---
layout: default
---

# ✍🏼 Unarity

* n-param => n(1-param)
* composition
* decoration
* **partial application**
* … 

<br>

```js {all|1-3|5-7}
// not so functional ...
const add = (x, y) => x + y;
[1,2,3].map(val => add(3, val))

// or
const add = x => y => x + y;
[1,2,3].map(add(3))
```

---
layout: default
---

# ✍🏼 Realworld Example Partial Application

* flexibility
* re-usability

```js{all|1-3|5-8|10-12|all}
// static get As data
const getDataApi = (endpoint, data, transformer) => api(endpoint, data, transformer);
getDataApi('http://A', data, transformer)

// reusable
const getDataApiA = partial(api, 'http://A');
getDataApiA(data, transformer);
...

const partial = (fn, ...currentArgs) =>
  (...laterUpcomingArgs) =>
  fn(...currentArgs, ...laterUpcomingArgs)
```

<!--
not fully evaluate fn
-->

---
layout: default
---

# ✍🏼 Strict Partial Application - Currying

* returns always functions which takes next param
* it will not receive the next n-params as pa does

<br>

```js{all|1-2|4|6-8|all}
// static get As data
const getDataApi = (endpoint, data, transformer) => api(endpoint, data, transformer);

const getDataApiA = curry(getDataApi)('http://A')(data)(transformer);

// take a look if you want to ;)
const curry = (fn, arity = fn.length, nextCurried) =>
  ...
```

---
layout: fact
---

# there is so much more
& libs (Ramda, Remeda, cycleJS, ...) & all the other topics

---
layout: fact
---

# starter served 🍛
maincourse incoming … & thanks for listening

---
layout: default
---

# most things are stolen

* [Lifting In Scala | Baeldung on Scala](https://www.baeldung.com/scala/lifting)
* [Scott Wlaschin](https://fsharpforfunandprofit.com/)
* [Functional Design Patterns](https://www.youtube.com/watch?v=srQt1NAHYC0)
* "Functional-Light JavaScript: Balanced, Pragmatic FP in JavaScript" by Kyle Simpson
* more…

---
layout: default
---

```js{all}
// parametrization - input-wizard
// userInputA
// if uIA <> null
//    userInputB
//    if uIB <> null
//        userInputC
//        if uIC <> null
//            final fn(uIA, uIB, uIC)
//        else None
//    else None
// else None

const ifVApply = (f, value) => value ? f(value) : None
const flow = pipe(
  ifVApply(),
  ifVApply(),
  ifVApply(),
)

```

---
layout: default
---

```js{all}
// Monadic Binds -> how combine missmatched functions 
//   two-track approach
//   fn with 1-in & two out to 2-in-out
//   fn input, parameter, output

// "core of a monad"
const bind = (nextFn, inputOption) => {
  if (inputOption.value) return nextFn(inputOption.value)
  else return null
}
```

<!--
3 Questions
1) Welche Programmierparadigmen kennst du und hast du ggf. schon angewendet?
2) Mit welchen funktionalen Sprachen hast du schon gearbeitet?
3) Welche Herausforderungen siehst du für dich in funktionaler Programmierung?

Monadic Binds -> how combine missmatched functions 
  two-track approach
  fn with 1-in & two out to 2-in-out
  fn input, parameter, output
map normal world to some other (mappable types are functors)
-->