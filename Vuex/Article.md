## How to consume API with Vuex and Axios

- Give Brief introduction to what Axios is
- Give Brief introduction on what Vuex is, advantage of vuex to passing props and params and other methods with code examples.
- What is state management and vuex state management pattern
- How to set up the simplest vuex store structure.
- When to use Vuex.
- Explain vuex index.
- Explain vuex action, when to use it with code samples
- Explain vuex mutation, when to use it with code samples
- Explain different vuex store structures with code samples and pictures.

### Give Brief introduction on what Vuex is, advantage of vuex to passing props and params and other methods with code examples

Vuex is a state management pattern plus library for Vue.js applications. It serves as a
centralized store for all the components in an application, it also integrates with Vue's official devtools extension to provide advanced features such as zero-config time-travel debugging and
state snapshot export / import.

For problem one, passing props can be tedious for deeply nested components, and simply doesn't work for sibling components. For problem two, we often find ourselves resorting to solutions such as reaching for direct parent/child instance references or trying to mutate and synchronize multiple copies of the state via events. Both of these patterns are brittle and quickly lead to unmaintainable code.

With Vuex we can extract the shared state out of components, and manage it in a global singleton. With this, our component tree becomes a big "view", and any component can access the state or trigger actions, no matter where they are in the tree!

                                            (DIAGRAM)

### What is state management and vuex state management pattern

State management is simply the management of the state of the application - or more importantly, the data that should be presented to the user at any given time. 

In an SPA (Single Page application) like Vue Js, multiple components may be interacting with the data at any given time - and changing it - before it is sent back to the server. Therefore a way to manage the changes - the state - of the data is needed. This reason births the vuex state management.

Vuex is a state management pattern that lets you extract shared state out of components, manage it in a global singleton and allow components access the state or trigger actions, no matter where they are in the tree!
                                            (DIAGRAM)

### How to set up the simplest vuex store structure with codes

- Vue Js Dev tool for chrome. If you don't have Vue Dev tools installed for chrome [install it here]()
- Vue CLI. If you don't have Vue CLI Installed already, run the following in your terminal;
```
npm install -g @vue/cli
``` 
To check if Vue CLI is already installed on your system. Run the code below on your terminal to check the version of Vue CLI installed, else Vue Js is not installed in your system.
```
vue --version
```

- Create a Vue project by running the following code in your terminal;

```
/** if you want to create the vue project in the folder you are currently on**/
vue create .

/**if you want to create a new folder for your vue app**/
vue create myApp

/**if you are using Vue CLI version lesser than 3.0**/
vue-init webpack myApp
```

- Install dependencies required for the project with the following codes;

```
/** to install vuex store for the project**/
npm install vuex

/**to install axios for handling http requests**/
npm install axios
```
Your folder structure should look like this;
                    (DIAGRAM)

#### Setting up the simplest vuex store structure.

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

### When to use Vuex with diagram and codes

Vuex helps us deal with shared state management with the cost of more concepts and boilerplate. It's a trade-off between short term and long term productivity.

If you've never built a large-scale SPA and jump right into Vuex, it may feel verbose and daunting. That's perfectly normal - if your app is simple, you will most likely be fine without Vuex. A simple store pattern may be all you need. But if you are building a medium-to-large-scale SPA, chances are you have run into situations that make you think about how to better handle state outside of your Vue components, and Vuex will be the natural next step for you.

Why you should use Vuex:

- If your components need to share and update state in many cases
- Vuex provides a single source of truth for data/state. This means APIs can be called once (single source of truth) and used by all components instead of calling the same API seperately for each component.
- No need to pass events up from one component and props down through multiple components when you have a state management.
- Global state is reactive which means updating state from one component allows it to be updated in every other component using it.



### Explain vuex index


### Explain vuex Action

In Vuex Instead of mutating the state, actions commit mutations. This means that while mutations alter/change states, actions perpertrate the change. Actions can contain arbitrary asynchronous operations, and are triggered with the ```store.dispatch``` method.

#### Key features

- Instead of mutating the state, actions commit mutations
- Actions can contain arbitrary asynchronous operations, this means operation need not be executed in sequence, code doesn't have to wait for an operation to execute – your program can continue to run
- Actions are triggered with the store.dispatch method
- You can dispatch actions in components with ```this.$store.dispatch('xxx')```, or use the mapActions helper which maps component methods to ```store.dispatch``` calls (requires root store injection)

To understand what Vuex Action is and how to use it, we are going to register a simple action that will consume API from json placeolder(online json folder).

```
// import dependency to handle HTTP request to our back end
import axios from 'axios'

//to handle state
const state = {
    books: []
}

//to handle state
const getters = {
    allBooks: (state) => state.books
}

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
```

- create a new component, i will name it ```"myStore"```, paste the following code into it

```
```
- serve your application by executing ```"npm run dev"``` on your terminal, navigate to ```"localhost:3000/myStore"``` to see your first vuex application created!

### Explain vuex Mutation
The only way to actually change state in a Vuex store is by committing a mutation. Vuex mutations are very similar to events: each mutation has a string type and a handler. The handler function is where we perform actual state modifications, and it will receive the state as the first argument.

#### Key Features

- One important rule to remember is that mutation handler functions must be synchronous
- You can commit mutations in components with this.$store.commit('xxx'), or use the mapMutations helper which maps component methods to store.commit calls (requires root store injection)

To understand what mutation is and how to use it, we are going to register a simple mutation that will consume API from json placeolder(online json folder).

```
// import dependency to handle HTTP request to our back end
import axios from 'axios'

//to handle state
const state = {
    books: []
}

//to handle state
const getters = {
    allBooks: (state) => state.books
}

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
```

- In your ```"myStore"``` folder, paste the following code into it

```
```
- serve your application by executing ```"npm run dev"``` on your terminal, navigate to ```"localhost:3000/myStore"``` to see your first vuex application created!

### Different vuex store structures.
```
├── index.html
└── src
    ├── components
    ├── App.vue
    └──store
       ├── index.js          # where we assemble modules and export the store
       ├── actions.js        # root actions
       ├── mutations.js      # root mutation
       ├── getters.js        # root getters
       └── ...
```