<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <div>
  <Header></Header>
  </div>
  <slot />
</template>

<style>
  body {
    background-color: #748bff;
    font-family: 'Roboto', sans-serif;
    margin: 0;
    overflow: hidden;
  }

</style>

<script>
import Header from "../components/header";
export default {
  components: {Header}
}
</script>