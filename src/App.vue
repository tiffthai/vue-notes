<template>
  <NoteList />
</template>

<script>
import NoteList from "./components/NoteList.vue";

export default {
  name: "App",
  components: {
    NoteList,
  },
};
</script>

<style>
html, body {
	width: 100%;
	height: 100%;
	margin: 0;
}

input, textarea {
	background: none;
	border: none;
	outline: none;
	font-size: 16px;
}

#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	width: 100%;
	height: 100%;
}
</style>
