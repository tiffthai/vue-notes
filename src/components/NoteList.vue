<template>
	<div>
		<div>
			<input v-model="userInput" @keyup.enter="addNote" />
			<button @click="addNote">Add note</button>
		</div>

		<div
			v-for="(listItem, listItemIndex) in listItems"
			:key="'item' + listItemIndex"
		>
			<input v-model="listItem.text" />
			<button @click="removeNote(listItemIndex)">delete</button>
		</div>
	</div>
</template>

<script>
export default {
	name: 'NoteList',
	data() {
		return {
			userInput: '',
			listItems: [
				{text: 'a'},
				{text: 'b'},
				{text: 'c'},
			]
		}
	},
	methods: {
		addNote() {
			let newNote = {
				text: this.userInput
			}
			this.listItems.push(newNote);

			this.userInput = '';
		},
		removeNote(listItemIndex) {
			this.listItems.splice(listItemIndex, 1);
		}
	}
}
</script>

<style>

</style>