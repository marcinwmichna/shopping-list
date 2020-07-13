<template>
  <div class="home">
    <h3>Shopping List</h3>
    <input id="add" v-model="newListText" @keydown.enter="add" @keydown.esc="resetPlaceholder" />

    <div class="item" v-for="(item, index) in items" :key="index">
      <div class="itemLeftBar"><button @click="deteleItem(index)">x</button></div>
      <div v-if="!item.editing">
        <div class="mainText" @click="enableEditing(index)">{{ item.name }}</div>
      </div>
      <div v-if="item.editing">
        <input
          v-model="editedListText"
          @keydown.enter="updateText(index)"
          @keydown.esc="resetPlaceholder()"
          @focusout="updateText(index)"
        />
      </div>
      <!--      <div v-once class="timeStamp">Created: {{ new Date() | moment() }}</div>-->
      <div class="timeStamp">Created: {{ item.dateCreated }}</div>
    </div>
  </div>
</template>

<script>
// let nextId = 0;
import moment from 'moment';

// let timeCreated = '';

export default {
  name: 'add',
  counter: 0,

  data() {
    return {
      newListText: '',
      editedListText: '',
      timeCreated: '',
      timeModified: '',
      items: [],
    };
  },

  methods: {
    enableEditing(index) {
      this.items[index].editing = true;
    },
    updateText(index) {
      this.items[index].name = this.editedListText;
      // this.editedListText = '';
      this.items[index].editing = false;
    },
    add() {
      // console.log('test');
      if (this.newListText !== '') {
        this.timeCreated = moment().format('DD-MM, h:mm');
        console.log(this.timeCreated);
        this.items.push({
          name: this.newListText,
          dateCreated: this.timeCreated,
          dateModified: this.timeModified,
          editing: false,
        });
        this.newListText = '';
      }
    },
    deteleItem(index) {
      this.items.splice(index, 1);
    },
    resetPlaceholder() {
      this.newListText = '';
      this.editedListText = '';
    },
  },
};
</script>
<style scoped>
.home {
  display: flex;
  flex-direction: column;
}
.itemLeftBar {
  margin-bottom: auto;
}
.timeStamp {
  margin-left: auto;
  /*margin: auto;*/
  font-size: 10px;
}
.mainText {
  padding: 5px;
  margin: auto;
  word-wrap: break-word;
  width: 250px;
}
button {
  margin: 5px;
}
input {
  width: 99%;
  border: 0;
  border-bottom: 1px solid black;
}

.item {
  border-radius: 2px;
  margin-top: 5px;
  display: flex;
  padding: 2px;
}
</style>
