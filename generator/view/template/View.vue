<template>
  <div>
    <h1><%= fileName %></h1>
    <div class="loader" v-show="loading"></div>
    <ul v-for="({ text }, i) in <%= fileName %>" :key="i">
      <li>{{ text }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: '<%= fileName %>',

  data() {
    return {
      <%= fileName %>: [],
      loading: true
    }
  },

  created() {
    window.fetch('/api/<%= viewName %>')
      .then(res => res.json())
      .then(<%= fileName %> => this.<%= fileName %> = <%= fileName %>)
      .finally(() => (this.loading = false))
  }
}
</script>

<style scoped>
  .loader {
    border-radius: 50%;
    border: 6px solid #f3f3f3;
    border-top: 6px solid #42ce35;
    width: 30px;
    height: 30px;
    -webkit-animation: spin 1s linear infinite; /* Safari */
    animation: spin 1s linear infinite;
  }

  @-webkit-keyframes spin {
    0% { -webkit-transform: rotate(0deg); }
    100% { -webkit-transform: rotate(360deg); }
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }
</style>
