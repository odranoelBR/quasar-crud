<template>
  <div id="q-app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>
<style lang="sass">
.q-markdown table
  border: none
.q-markdown table td:nth-child(1)
  color: $teal-9
.q-markdown table tr
  background: $teal-3
  border: none
.q-markdown table thead tr th
  border: none
.q-markdown table td
  border: none
.q-markdown table tr
  background: white
.q-markdown table tr:nth-child(odd)
  background: $teal-3
</style>