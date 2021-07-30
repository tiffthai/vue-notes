<template>
	<div id="noteList">
		<div id="noteHeadersContainer">
			<div id="addNewNoteWrapper">
				<input 
					v-model="userInput" 
					placeholder="add new note"
					@keyup.enter="addNote" 
					id="addNoteInput"
				/>
				<button @click="addNote">Add note</button>
			</div>

			<div
				v-for="(listItem, listItemIndex) in listItems"
				:key="'item' + listItemIndex"
				:class="{activeListItem: listItemIndex === activeIndex}"
				class="listItem"
			>
				<input 
					v-model="listItem.header" 
					@focus="handleOpenNoteContents(listItemIndex)" 
					class="noteHeaderInput"
				/>
				<button @click="removeNote(listItemIndex)">delete</button>
			</div>
		</div>

		<div id="noteDescriptionContainer">
			<h2>{{ noteHeader }}</h2>
			<div>
				<textarea 
					v-if="listItems.length"
					:value="noteDescription" 
					id="noteDescriptionTextarea"
				/>
			</div>

			<div id="descriptionActionContainer">
				<button>revert</button>
				<button>save edit</button>
			</div>
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
				{header: 'header a', text: 'description of note goes here'},
				{header: 'header b', text: 'description of note goes here'},
				{header: 'header c', text: 'description of note goes here'},
			],
			activeIndex: 0
		}
	},
	computed: {
		noteHeader() {
			return this.listItems[this.activeIndex].header;
		},
		noteDescription() {
			return this.listItems[this.activeIndex].text;
		}
	},
	methods: {
		addNote() {
			let newNote = {
				header: this.userInput,
				text: ''
			}
			this.listItems.push(newNote);

			this.userInput = '';
		},
		removeNote(listItemIndex) {
			this.listItems.splice(listItemIndex, 1);
		},
		handleOpenNoteContents(listItemIndex) {
			this.activeIndex = listItemIndex;
		}
	}
}
</script>

<style lang="scss" scoped>
#noteList {
	width: 100%;
	height: 100%;
	display: flex;
}

// left column styles
#noteHeadersContainer {
	flex: 3;
	border-right: 2px solid #E9E9E9;
}

#addNewNoteWrapper {
	padding: 12px 12px 36px 12px;
	display: flex;
}

#noteDescriptionContainer {
	flex: 2;
	padding: 12px;
}

#addNoteInput {
	background: #E9E9E9;
	border-radius: 4px;
	padding: 8px;
}

.listItem {
	border-bottom: 1px solid #E9E9E9;
	padding: 4px 12px;
	display: flex;
}

.activeListItem {
	background:#CBE5D5;
}

.noteHeaderInput {
	width: 100%;
}

// right column styles
#noteDescriptionTextarea {
	width: 100%;
	height: 100%;
	resize: none;
}

#descriptionActionContainer {
	display: flex;
	justify-content: space-between;
}
</style>