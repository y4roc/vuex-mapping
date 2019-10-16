# Vuex Mapping

Vuex-Mapping is an easy way to map references between two and more objects.

## Installation

```shell script
npm install vuex-mapping

yarn add vuex-mapping
```

## Using

```ecmascript 6
import Vue from 'vue'
import Vuex from 'vuex'
import mapping from 'vuex-mapping'

Vue.use(Vuex)

const store = new Vuex.Store({
  plugins: [mapping],
  ...
})

new Vue({
  store,
  ...
})
```

## Working with it

Vuex-Mapping is listing on each mutation and action. It get the payload and looks for objects with property `id` and `__typename`. In `__typename` should be the type of the model.

## Example

```ecmascript 6
// create an user
commit('saveUser', {
  id: 1,
  username: 'Bob',
  group: {
    id: 1,
    __typename: 'Group'
  },
  __typename: 'User'
})

// create a group
commit('saveGroup', {
  id: 1,
  name: 'Admin',
  __typename: 'Group'
})

// update a group
commit('saveGroup', {
  id: 1,
  description: 'Sleeping all time',
  __typename: 'Group'
})

// create a second user
commit('saveUser', {
  id: 2,
  username: 'Ann',
  group: {
    id: 1,
    __typename: 'Group'  
  },
  __typename: 'User'
})

// Get saved users
let bob = action('loadUserById', 1)
let ann = action('loadUserById', 2)

/* Output should be:
 * {id: 1, username: 'Bob', group: {id: 1, name: 'Admin', description: 'Sleeping all time', __typename: 'Group'}}
 * {id: 2, username: 'Ann', group: {id: 1, name: 'Admin', description: 'Sleeping all time', __typename: 'Group'}}
 */
console.log(bob)
console.log(ann)
```
