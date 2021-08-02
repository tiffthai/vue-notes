<template>
    <div id="noteList">
        <div id="noteHeadersContainer">
			<div id="title">
				<h2>Vue Notes</h2>
			</div>
            <div id="addNewNoteWrapper">
                <input
                    v-model="userInput"
                    placeholder="add new note"
                    @keyup.enter="addNote"
                    id="addNoteInput"
                />
                <button @click="addNote">
                    <img src="@/assets/add.svg" />
                </button>
            </div>

            <div
                v-for="(listItem, listItemIndex) in listItems"
                :key="'item' + listItemIndex"
                :class="{ activeListItem: listItemIndex === activeIndex }"
                class="listItem"
            >
                <input
                    v-model="listItem.header"
                    @focus="handleOpenNoteContents(listItemIndex)"
                    class="noteHeaderInput"
                />
                <button @click="removeNote(listItemIndex)">
                    <img src="@/assets/delete.svg" />
                </button>
            </div>
        </div>

        <div id="rightColumn">
            <div id="noteDetailsContainer">
                <h2>{{ noteHeader }}</h2>
                <div id="descriptionWrapper">
                    <textarea
                        v-if="listItems.length"
                        v-model="currentNoteDescription"
						ref="noteDescriptionTextarea"
						@input="updateNoteDescription"
                        id="noteDescriptionTextarea"
						placeholder="description of note goes here"
                    />
                </div>
            </div>

            <div id="descriptionActionContainer">
                <button @click="revertNoteDescription">
                    <img src="@/assets/revert.svg" />
                </button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "NoteList",
    data() {
        return {
            userInput: "",
            listItems: [
                { header: "header a", text: "" },
                { header: "header b", text: "" },
                { header: "header c", text: "" },
            ],
            activeIndex: 0,
			originalNote: "",
			currentNoteDescription: ""
        };
    },
    computed: {
        noteHeader() {
            return this.listItems[this.activeIndex].header;
        }
    },
    methods: {
        addNote() {
            let newNote = {
                header: this.userInput,
                text: "",
            };
            this.listItems.push(newNote);

            this.userInput = "";
        },
        removeNote(listItemIndex) {
            this.listItems.splice(listItemIndex, 1);
        },
        handleOpenNoteContents(listItemIndex) {
            this.activeIndex = listItemIndex;
			this.currentNoteDescription = this.listItems[listItemIndex].text;
			this.originalNote = this.listItems[listItemIndex].text;

			this.$nextTick(() => {
				this.$refs.noteDescriptionTextarea.focus();
			})
        },
		updateNoteDescription() {
			this.listItems[this.activeIndex].text = this.currentNoteDescription;	
		},
		revertNoteDescription() {
			this.currentNoteDescription = this.originalNote;
			this.listItems[this.activeIndex].text = this.originalNote;
		}
    },
	mounted() {
		this.currentNoteDescription = this.listItems[0].text;

		if (this.listItems.length) {
			this.$refs.noteDescriptionTextarea.focus();
		}
	}
};
</script>

<style lang="scss" scoped>
img {
    width: 16px;
}

#noteList {
    width: 100%;
    height: 100%;
    display: flex;
}

// left column styles
#noteHeadersContainer {
    flex: 3;
    border-right: 2px solid #e9e9e9;

	#title {
		padding: 0px 12px;
	}

	#addNewNoteWrapper {
    padding: 0px 12px 24px 12px;
    display: flex;
	align-items: center;

		#addNoteInput {
			width: 100%;
			background: #e9e9e9;
			border-radius: 4px;
			padding: 8px;
		}

		button {
			width: 28px;
			height: 28px;
			background: #89a995;
			border-radius: 50%;
			display: flex;
			align-items: center;
			justify-content: center;
			margin-left: 4px;

			&:hover {
				background: #789482;
			}
		}
	}

	.noteHeaderInput {
		width: 100%;
	}
}

.listItem {
	border-bottom: 1px solid #e9e9e9;
	padding: 4px 12px;
	display: flex;

	&:hover {
		transition: .3s ease;
		background: #ECF5EF;
	}
}

.activeListItem {
	background: #cbe5d5;
}

// right column styles
#rightColumn {
    flex: 2;
    padding: 12px;
    display: flex;
    flex-direction: column;

    #noteDetailsContainer {
        display: flex;
        flex-direction: column;
        height: 100%;

        #descriptionWrapper {
            height: 100%;
        }
    }

	#descriptionActionContainer {
		height: 40px;
		display: flex;
		align-items: center;
		justify-content: flex-end;
	}
}

#noteDescriptionTextarea {
    width: 100%;
    height: 100%;
    resize: none;
}
</style>