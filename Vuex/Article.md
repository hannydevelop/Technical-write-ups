## How to consume API with Vuex and Axios

Only a few frameworks have built-in HTTP APIs. Angular 2 has the ```HTTP module```, JQuery has ```$ajax```, and up until Vue 2.0, Vue js had ```Vue-resource```. In Vue 2.0, the developers decided that having a built-in HTTP client module was rather redundant, and could be better serviced by third-party libraries. The alternative most frequently recommended is ```Axios```.  
Axios is a great HTTP client library, It uses promises by default and runs on both the client and the server (which makes it appropriate for fetching data during server-side rendering). It’s also quite easy to use with Vue

For problem one, passing props can be tedious for deeply nested components. For problem two, we often find ourselves resorting to solutions such as reaching for direct parent/child instance references or trying to mutate and synchronize multiple copies of the state via events. Both of these patterns are brittle and quickly lead to unmaintainable code.

Vuex is a state management pattern plus library for Vue.js applications, It serves as a centralized store for all the components in an application.

 ```
this image below was copied from https://www.vuemastery.com/courses/mastering-vuex/intro-to-vuex/
```                               
![0_5BcWxyQW7ai1JsVd.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1600190773034/QSSgxtz0Z.gif)

### Understanding state management and vuex state management pattern

State management is simply the management of the state of the application or more importantly, the data that should be presented to the user at any given time. 

In an SPA (Single Page application) like Vue Js, multiple components may be interacting with the data at any given time and changing it before sending the data back to the server. Therefore a way to manage the changes, "the state" of the data is needed. This reason births the vuex state management.

Vuex is a state management pattern that lets you extract shared state out of components, manage it in a global singleton and allow components access the state or trigger actions, no matter where they are in the tree!

### How to set up the simplest vuex store structure with codes

- You need Vue CLI to create your Vue app. If you don't have Vue CLI Installed already, run the following in your terminal;
```
npm install -g @vue/cli
``` 
To check if Vue CLI is already installed on your system. Execute the code below on your terminal to check the version of Vue CLI installed, you should get a Vue version else Vue  is not installed in your system.
```
vue --version
2.9.6
```

- Create a Vue project by running the following code in your terminal;

```
/** if you want to create the vue project in the folder you 
are currently on, use this code**/
vue create .

/**if you want to create a new folder for your vue app, 
you should use this code**/
vue create myApp

/**if you are using Vue CLI version lesser than 3.0 use this code.**/
vue-init webpack myApp
```
- Answer the questions as shown in the image below, to create your Vue app.
![vue2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1600190035413/tk_AdsCSz.png)

- Install dependencies required for the project with the following codes;

```
/** to install vuex store for the project**/
npm install vuex

/**to install axios for handling http requests**/
npm install axios
```

### When to use Vuex

If you have never built a large-scale SPA and jump right into Vuex, it may feel verbose and daunting. This is perfectly normal - if your app is simple, you will most likely be fine without Vuex. But if you are building a medium-to-large-scale SPA, chances are you have run into situations that make you think about how to better handle state outside of your Vue components, and Vuex will be the natural next step for you.

Why you should use Vuex:

- If your components need to share and update state in many cases
- Vuex provides a single source of truth for data/state.
- No need to pass events up from one component and props down through multiple components when you have a state management.
- Global state is reactive which means altering state allows it to be updated in every other component using it.

### Vuex Store

#### 1. Setting up the simplest vuex store structure.

- create a folder in your ```"src"``` folder and name it ```"store"```
- In your store folder create a file and name it ```"index.js"```.

```
├── index.html
└── src
    ├── components
    ├── App.vue
    └──store
       └── index.js          # where we assemble modules and export the store
```
- In your store/index.js file, input the following code;

```
// import dependency to handle HTTP request to our back end
import axios from 'axios'

//to handle state
const state = {}

//to handle state
const getters = {}

//to handle actions
const actions = {}

//to handle mutations
const mutations = {}

//export store module
export default {
    state,
    getters,
    actions,
    mutations
}
/** we have just created a boiler plate for our vuex store module**/
```

- In your main.js file, register your store by adding the following codes to your main.js file;

```
//add this line to your main.js file
import store from './store'

new Vue({
//add this line to your main.js file
store,
render: h => h(App)
})
//other lines have already been added to your main.js file by default
```

#### 2. Vuex Actions Explained and Mutations Explained

In Vuex Actions, Instead of mutating the state, actions commit mutations. This means that while mutations alter/change states, actions perpertrate the change. Actions can contain arbitrary asynchronous operations, and are triggered with the ```store.dispatch``` method.

#### Key features

- Instead of mutating the state, actions commit mutations
- Actions can contain arbitrary asynchronous operations, this means operation need not be executed in sequence, code doesn't have to wait for an operation to execute – your program can continue to run
- Actions are triggered with the store.dispatch method
- You can dispatch actions in components with ```this.$store.dispatch('xxx')```, or use the mapActions helper which maps component methods to ```store.dispatch```.

The only way to actually change state in a Vuex store is by committing a mutation. Vuex mutations are very similar to events: each mutation has a string type and a handler. The handler function is where we perform actual state modifications, and it will receive the state as the first argument.

#### Key Features

- One important rule to remember is that mutation handler functions must be synchronous
- You can commit mutations in components with ```this.$store.commit('xxx')```, or use the mapMutations helper which maps component methods to ```store.commit```.
To understand what mutation and actions are and how they are used, we are going to register a simple mutation that will consume API from JSONplaceolder(Fake Online REST API for Testing and Prototyping).

```
// import dependency to handle HTTP request to our back end
import axios from 'axios'
import Vuex from 'vuex'
import Vue from 'vue'

//load Vuex
Vue.use(Vuex);

//to handle state
const state = {
    posts: []
}

//to handle state
const getters = {}

//to handle actions
const actions = {
    getPosts({ commit }) {
        axios.get('https://jsonplaceholder.typicode.com/posts')
            .then(response => {
                commit('SET_POSTS', response.data)
        })
    }
}

//to handle mutations
const mutations = {
    SET_POSTS(state, posts) {
        state.posts = posts
    }
}

//export store module
export default new Vuex.Store({
    state,
    getters,
    actions,
    mutations
})
```

- create a new component, i will name it ```"myStore"```, paste the following code into it

```
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div v-for='post in posts' :key='post.id'>
  <h3>Post Title: </h3>  {{post.title}}
      <h3>Post Body: </h3>{{post.body}}
    </div>
    <h2>Essential Links</h2>
  </div>
</template>

<script>
export default {
  name: 'myStore',
  data () {
    return {
      msg: 'Welcome to my Vuex Store'
    }
  },
  computed: {
    posts() {
    return this.$store.state.posts
    }
  },
  mounted() {
    this.$store.dispatch("getPosts");
  }
}
</script>
```
- serve your application by executing ```"npm run dev"``` on your terminal, navigate to ```"localhost:8080/myStore"``` to see your first vuex application created!

![vuee1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1600190098151/A-Mcq-SWv.png)

#### 3. vuex Getters Explained

Sometimes we may need to compute derived state based on store state, Vuex allows us to define "getters" in the store. You can think of them as computed
properties for stores. Like computed properties, a getter's result is cached based on its
dependencies, and will only re-evaluate when some of its dependencies have changed.

#### Key Features

- Getters will receive the state as their 1st argument
- Getters will also receive other getters as the 2nd argument
- The mapGetters helper simply maps store getters to local computed properties

To understand what getters is and how to use it, we are going to compute a derived state based on our store state by hot-coding our state;

```
// import dependency to handle HTTP request to our back end
import Vuex from 'vuex'
import Vue from 'vue'

//load Vuex
Vue.use(Vuex);

//to handle state
const state = {
    products: [
       {
           id: 1,
           title: 'Shirt',
           price: '$40'
       },
        {
           id: 2,
           title: 'Trouser',
           price: '$10'
       },
   ]
}

//to handle state
const getters = {
    allProducts: (state) => state.products
}

//to handle actions
const actions = {}

//to handle mutations
const mutations = {}

//export store module
export default new Vuex.Store({
    state,
    getters,
    actions,
    mutations
})
```

- In your ```"myStore"``` folder, paste the following code into it

```
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div v-for="product in products" :key="product.id">
      {{product.title}}, {{product.price}}
      </div>
  </div>
</template>

<script>
/*
import { mapGetters } from 'vuex'; //This is 
another method for mapGetters Helper
*/
export default {
  name: "myStore",
  data() {
    return {
      msg: "Welcome to my Vuex Store Getter example",
    };
  },
  computed: {
    products() {
      return this.$store.getters.allProducts;
    },
  },
  /* 
  computed: mapGetters(['allProducts']) //This is 
another method for mapGetters Helper
  */
};
</script>
```
- serve your application by executing ```"npm run dev"``` on your terminal, navigate to ```"localhost:8080/myStore"``` to see your first vuex application created!

![vuee2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1600190123825/zgOx0JHNu.png)


### Consuming APIs with Vuex and Axios, Harnessing Actions, Mutations, State and Getters.

To understand properly how to create a Vuex store and consume APIs with Axios, using Vuex Actions, State, Mutation and Getters we would create a simple Vue application that fetches user information from our fake json backend.

```
// import dependency to handle HTTP request to our back end
import axios from 'axios'
import Vuex from 'vuex'
import Vue from 'vue'

//load Vuex
Vue.use(Vuex);

//to handle state
const state = {
    users: []
}

//to handle state
const getters = {
    allUsers: (state) => state.users
}

//to handle actions
const actions = {
    getUsers({ commit }) {
        axios.get('https://jsonplaceholder.typicode.com/users')
            .then(response => {
                commit('SET_USERS', response.data)
           })
    }
}

//to handle mutations
const mutations = {
    SET_USERS(state, users) {
        state.users = users
    }
}

//export store module
export default new Vuex.Store({
    state,
    getters,
    actions,
    mutations
})
```
- In your ```"myStore"``` folder, paste the following code into it

```
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>Made By Getters</h1>
  <div v-for='gettersuser in gettersusers' :key='gettersuser.id'>
    {{gettersuser.id}} {{gettersuser.name}} {{gettersuser.address}}
    </div>
    <h1>Made By Actions</h1>
  <div v-for='user in users' :key='user.id'>
    {{user.id}} {{user.name}} {{user.address}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'myStore',
  data () {
    return {
      msg: 'Welcome to my Vuex Store'
    }
  },
  computed: {
    gettersusers() {
    return this.$store.getters.allUsers
    },
    users() {
    return this.$store.state.users
    }
  },
  mounted() {
    this.$store.dispatch("getUsers");
  }
}
</script>
```
- serve your application by executing ```"npm run dev"``` on your terminal, navigate to ```"localhost:8080/myStore"``` to see your first vuex application created!

![vuee3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1600190154254/zpmO68tcO.png)

### Different vuex store structures.

This is the simplest vuex store structure, Actions, Getters, State and mutation are called and exported in the ```index.js file```.

```
├── index.html
└── src
    ├── components
    ├── App.vue
    └──store
       └── index.js          # where we assemble modules and export the store
```

As your application becomes bigger, there may be need to separate Actions, Mutations, Getters and State modules into their different files. 

```
├── index.html
└── src
    ├── components
    ├── App.vue
    └──store
       ├── index.js          # where we assemble modules and export the 
       ├── actions.js        # root actions
       ├── mutations.js      # root mutation
       ├── getters.js        # root getters
       └── state
```

Due to using a single state tree, all states of our application are contained inside one big object. 
However, as our application grows in scale, the store can get really bloated.
To help with that, Vuex allows us to divide our store into modules. Each module can contain its own state, mutations, actions, getters, and even nested modules.

```
├── index.html
├── main.js
├── api
│   └── ... # abstractions for making API requests
├── components
│   ├── App.vue
│   └── ...
└── store
    ├── index.js          # where we assemble modules and export the store
    ├── actions.js        # root actions
    ├── mutations.js      # root mutations
    └── modules
        ├── cart.js       # cart module
        └── products.js 
```

### Conclusion

In this tutorial, we have successfully looked at what state management is and why you need Vuex for your Vue applications. We have looked at what the Vuex store comprises of and what Actions, Mutations, Getters, and State mean in Vuex.

We have created a simple Vue application to demonstrate Vuex and have also explained the different Vuex store structure and which is best for your application. 

Thank you so much for reading this article till the end! you can contact me on [twitter](http://www.twitter.com/hannydevelop) or send a [mail](ukpaiugochi0@gmail.com) if you have any questions regarding this article or suggestions.