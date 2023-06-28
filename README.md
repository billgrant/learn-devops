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

