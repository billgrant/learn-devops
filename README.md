# learn-devops

I was inspired by this [post](https://www.reddit.com/r/devops/comments/14hl4ha/comment/jpcampc/?utm_source=share&utm_medium=web2x&context=3). Coming from Network Engineering > Network Automation > Pre-sales Engineering. I realized that while I worked on most of these technologies I have never build application from scratch like is suggested in the post. So here we go.

1. Write a web application in Vue.

I chose Vue because it is 100% new to me.

I am starting by picking out the first tutorial in Vue that Google returned [Getting started with Vue](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_getting_started)

## Getting Started

```shell
vue create moz-todo-vue
```

I know nothing about Vue at this point, but man that is a lot of files. 

After some clunking around here is code in `App.vue`

```Vue
<template>
    <div id="app">
      <h1>To-Do-List</h1>
    </div>
  </template>

<script>
export default {
  name: 'App',
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
```

## Creating my first Vue component

Moving onto the next step. This entire Vue app build will be a carbon copy of the tutorial linked above. This will hopefully get interesting later when I attempt to build the API.

I create a file called `ToDoItem.vue` under `web-application/moz-todo-vue/src/components` with the following contents

```vue
<template>
    <div>
        <input type="checkbox" id="id" v-bind:checked="isDone" />
        <label for="id">{{ label }}</label>
    </div>
</template>
<script>
import uniqueId from "lodash/uniqueId";

export default {
  props: {
    label: { required: true, type: String },
    done: { default: false, type: Boolean },
  },
  data() {
    return {
      isDone: this.done,
      id: uniqueId("todo-"),
    };
  },
};

</script>
```

This is what the `App.vue` file looks like now.

```vue

  <template>
    <div id="app">
      <h1>To-Do-List</h1>
      <ul>
        <li>
          <to-do-item label="My ToDo Item" :done="true"></to-do-item>
        </li>
      </ul>
    </div>
  </template>

<script>

import ToDoItem from "./components/ToDoItem.vue";

export default {
  name: 'App',
  components: {
    ToDoItem
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

At this point. We have a ToDo list app that we can add multiple list items to. Each item will have a unique id and and can be
set to checked or uncheck when the application starts.

## Rendering a list of Vue components

Instead of single component we now have a list of components that app loops through. They each have a unique id.

`App.vue`

```vue

  <template>
    <div id="app">
      <h1>To-Do-List</h1>
      <ul>
        <li v-for="item in ToDoItems" :key="item.id">
          <to-do-item 
            v-bind:label="item.label" 
            :done="item.done"
            :id="item.id"></to-do-item>
        </li>
      </ul>
    </div>
  </template>

<script>

import ToDoItem from "./components/ToDoItem.vue";
import uniqueId from "lodash/uniqueId";

export default {
  name: 'App',
  components: {
    ToDoItem
  },
  data() {
    return {
      ToDoItems: [
        { id: uniqueId("todo-"), label: "Learn Vue", done: false },
        { id: uniqueId("todo-"), label: "Create a Vue project with the CLI", done: true },
        { id: uniqueId("todo-"), label: "Have fun", done: true },
        { id: uniqueId("todo-"), label: "Create a to-do list", done: false },
      ],
    };
   },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

`ToDoItem.vue`

```vue
<template>
    <div>
        <input type="checkbox" id="id" v-bind:checked="isDone" />
        <label for="id">{{ label }}</label>
    </div>
</template>
<script>

export default {
  props: {
    label: { required: true, type: String },
    done: { default: false, type: Boolean },
    id: { required: true, type: String },
  },
  data() {
    return {
      isDone: this.done,
    };
  },
};

</script>
```