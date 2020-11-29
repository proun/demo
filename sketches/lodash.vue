<template>
  <div>Zip result is</div>
</template>

<script lang="ts" type="module">
import zip from '../node_modules/lodash-es/zip.js'

const text = JSON.stringify(zip(['a', 'c'], [1, 3], [true, false]))
const newDiv = document.createElement('div')
newDiv.innerHTML = text
document.body.appendChild(newDiv)
</script>

<style>
* {
  color: rgb(73, 7, 255);
}
</style>