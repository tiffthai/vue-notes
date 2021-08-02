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
	font-family: 'Lato', sans-serif;
}

input, textarea {
	background: none;
	border: none;
	outline: none;
	font-size: 16px;
	font-family: 'Lato', sans-serif;
}

button {
	border: none;
	background: transparent;
	display: flex;
}

button:hover {
	transition: .3s ease;
	cursor: pointer;
}

h2 {
	font-weight: 400;
}

#app {
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	width: 100%;
	height: 100%;
}
</style>
