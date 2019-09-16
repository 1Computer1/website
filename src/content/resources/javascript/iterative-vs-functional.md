---
authors:
  - "veksen#1060"
created_at: "2019/07/27"
title: Iterative vs Functional array helpers
---

This article assumes that you are comfortable with the very basics of JavaScript arrays, and how they differ to objects.

## Getting a specific element using `find()`

It's not rare to need to look for some specific element based on a criteria. `find()` makes this particularly easy. It takes a function, taking a few arguments:

- current item
- index of current item
- original array reference

If that function evaluates to truthy, this item is returned, and the loop ends.

If you're only interested in the presence of an element, consider using `some()`, which instead returns a boolean.

Conventionally, in an iterative approach, this would be done using a preset variable, and looping through our array.

```js
// given our data
const users = [
  { name: "Joe", age: 25 },
  { name: "John", age: 17 },
  { name: "Jane", age: 16 },
]

// functional way
const foundUser = users.find(user => user.name === "John")

// iterative way
let foundUser = null
users.forEach(user => {
  if (user.name === "John") {
    foundUser = user
  }
})
```

## Keep specific items using `filter()`

`filter()` makes it easy to keep specific items based on a criteria.

It takes a function, taking a few arguments:

- current item
- index of current item
- original array reference

If that function evaluates to truthy, this specific item is kept, otherwise it is removed.

`filter()` does not modify (mutate) the original array, instead, it returns a new one.

```js
// given our data
const users = [
  { name: "Joe", age: 25 },
  { name: "John", age: 17 },
  { name: "Jane", age: 16 },
]

// functional way
const youngerUsers = users.filter(user => user.age < 18)

// iterative way
const youngerUsers = []
users.forEach(user => {
  if (user.age < 18) {
    youngerUsers.push(user)
  }
})
```

## Modifying all elements of an array using `.map()`

It's common to want to modify every element of an array with some logic, and `map()` makes this easy.

It takes a function, taking a few arguments:

- current item
- index of current item
- original array reference (rarely used)
- current reference to `this` (rarely used)

```js
// given our data
const users = [
  { name: "Joe", age: 25 },
  { name: "John", age: 17 },
  { name: "Jane", age: 16 },
]

// functional way
const userNames = users.map(user => user.name)

// iterative way
const userNames = []
users.forEach(user => {
  userNames.push(user.name)
})
```

## Running custom logic using an array using `.reduce()`

`reduce()` is often less understood, but it's not that complicated once you get the basics. Itself, it takes 2 arguments, a function, and an initial value. The function takes a few arguments:

- accumulator, that is a reference to the current value that was last returned, or the initial value
- current value, the currently looped element
- current index
- original array

```js
// given our data
const users = [
  { name: "Joe", age: 25 },
  { name: "John", age: 17 },
  { name: "Jane", age: 16 },
]

// functional way
const totalAge = users.reduce((acc, user) => acc + user.age, 0)

// iterative way
let totalAge = 0
users.forEach(user => {
  totalAge += user.age
})
```

## Checking if any element matches a condition with `some()`

`some()` is very similar to `find()`, except it returns a boolean on a match.

Conventionally, we would prepare some variable with a value of false, loop over all of the elements, and exit the loop once we find a match.

```js
const users = [
  { name: "Joe", age: 25 },
  { name: "John", age: 17 },
  { name: "Jane", age: 16 },
]
```

Iterative way:

```js
let hasYoungUsers = false
for (let i = 0; users.length > i; i++) {
  if (user > 18) {
    hasYoungUsers = true
    break
  }
}
```

Functional way:

```js
const hasYoungUsers = users.some(user => user.age < 18)
```

## every

```js
const users = [
  { name: "Joe", age: 25 },
  { name: "John", age: 17 },
  { name: "Jane", age: 16 },
]
```

Iterative way:

```js
let allUsersAreOldEnough = true
for (let i = 0; users.length > i; i++) {
  if (user.age > 18) {
    allUsersAreOldEnough = false
    break
  }
}
```

Functional way:

```js
const hasYoungUsers = users.every(user => user.age < 18)
```

## includes

```js
const pets = ["cat", "dog", "bat"]
```

Iterative way:

```js
let found = false
pets.forEach(pet => {
  if (pet === "dog") {
    found = true
  }
})

// or most of the time done with indexOf
pets.indexOf("dogs") > 0
```

Functional way:

```js
pets.includes("dogs")
```
