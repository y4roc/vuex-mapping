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
```

## Working with it

Vuex-Mapping is listing on each mutation and action. It get the payload and looks for objects with property `id` and `__typename`. In `__typename` should be the type of the model.

## Example

```ecmascript 6
commit('update', {
  id: 1,
  username: 'Bob',
  group: {
    id: 1,
    __typename: 'Group'
  }
})

commit('update', {
  id: 1,
  name: 'Admin',
  __typename: 'Group'
})

// Get saved user
let user = action('loadUser')

/* Output should be:
 * {id: 1, username: 'Bob', group: {id: 1, name: 'Admin', __typename: 'Group'}}
 */
console.log(user)
```
