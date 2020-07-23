<template
  ><div class="body">
    <div class="headerWrapper">
      <header class="header">
        <span>{ to</span>
        <span><b>BUY </b>}</span>
      </header>
    </div>
    <div class="home">
      <input
        placeholder="Add new item"
        class="mainInput"
        cols="14"
        id="add"
        v-model="newListText"
        @keydown.enter="addItem"
        @keydown.esc="resetPlaceholder"
      />
      <div class="listWrap">
        <!--    <b-alert show> Hello {{ name }}! </b-alert>-->
        <div fluid class="item" v-for="(item, index) in items" :key="index">
          <div class="leftWrap">
            <!--              <button class="deteleBtn" @click="deteleItem(index)">X</button>-->
            <svg
              @click="deteleItem(index)"
              class="inline deteleBtn"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12 19 6.41z"
                id="Close"
                fill="#999999"
              />
            </svg>
            <div class="inline" v-if="!item.editing.name">
              <div class="mainText" @click="enableEditing(index)">
                {{ item.name }}
              </div>
            </div>
            <div class="itemInput inline" v-if="item.editing.name">
              <input
                class="editInput"
                type="text"
                v-focus
                v-model="editedListText"
                @keydown.enter="updateText(index)"
                @keydown.esc="resetPlaceholder()"
                @focusout="updateText(index)"
              />
            </div>
          </div>
          <div class="rightWrap">
            <div class="amountCounter inline">
              {{ item.amount }}
            </div>

            <svg
              @click="updateModTime(index)"
              v-on:click="addAmount(index)"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M 11 2 L 11 11 L 2 11 L 2 13 L 11 13 L 11 22 L 13 22 L 13 13 L 22 13 L 22 11 L 13 11 L 13 2 Z"
                fill="#999999"
              />
            </svg>

            <svg
              @click="updateModTime(index)"
              v-on:click="subtractAmount(index)"
              viewBox="0 0 409.6 409.6"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M392.533,187.733H17.067C7.641,187.733,0,195.374,0,204.8s7.641,17.067,17.067,17.067h375.467c9.426,0,17.067-7.641,17.067-17.067S401.959,187.733,392.533,187.733z"
                fill="#999999"
              />
            </svg>
            <div class="created-edited inline">
              <label class="timeStamp">Created: {{ item.dateCreated }}</label>
              <label class="timeStamp">Edited: {{ item.dateModified }}</label>
            </div>
          </div>
        </div>
      </div>
    </div>
    <footer class="footerWrapper">
      <div class="footer">
        <div></div>
        <div class="rightFooter">
          <a target="_blank" href="https://github.com/marcinwmichna/shopping-list">
            <img class="socialMedia" src="https://img.icons8.com/fluent/50/000000/github.png" />
          </a>
          <a target="_blank" href="https://www.linkedin.com/in/marcin-michna-685732185/">
            <img class="socialMedia" src="https://img.icons8.com/color/48/000000/linkedin.png" />
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import moment from 'moment';

const focus = {
  inserted(el) {
    el.focus();
  },
};

export default {
  name: 'add',
  counter: 0,

  directives: {
    focus,
  },
  data() {
    return {
      newListText: '',
      editedListText: '',
      timeCreated: '',
      timeModified: '',
      amount: '',
      items: [
        {
          name: 'Pieczywo',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 1,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Sok pomarańczowy',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 2,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Ser żółty',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 1,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Ciastka z czekoladą',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 10,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Pomidory',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 3,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Czosnek',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 1,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Sałata',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 1,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Ser pleśniowy',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 1,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Papryka',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 2,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Mleko',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 4,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Jogurt naturalny 0%',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 3,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Tofu',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 2,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Kukurydza',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 6,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Hummus',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 2,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Kabanosy',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 3,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Szpinak mrożony',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 2,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Cukier',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 20,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Cukierki',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 40,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Lody',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 3,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Krewetki',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 1,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
        {
          name: 'Kwiaty',
          dateCreated: moment().format('DD-MM, h:mm'),
          dateModified: 'none',
          amount: 2,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
        },
      ],
    };
  },
  methods: {
    subtractAmount(index) {
      if (this.items[index].amount > 1) {
        this.items[index].amount -= 1;
      }
    },
    addAmount(index) {
      this.items[index].amount += 1;
    },
    updateModTime(index) {
      this.items[index].dateModified = moment().format('DD-MM, h:mm');
    },
    desactivate(index) {
      this.items[index].display = false;
    },
    enableEditing(index) {
      this.items[index].editing.name = true;
      this.editedListText = this.items[index].name;
    },
    updateText(index) {
      this.items[index].name = this.editedListText;
      this.items[index].editing.name = false;
      this.items[index].dateModified = moment().format('DD-MM, h:mm');
      if (this.editedListText === '') {
        this.deteleItem(index);
      }
    },
    addItem() {
      // console.log('test');
      if (this.newListText !== '') {
        this.timeCreated = moment().format('DD-MM, h:mm');
        this.items.push({
          name: this.newListText,
          dateCreated: this.timeCreated,
          dateModified: 'none',
          amount: 1,
          editing: {
            name: false,
            amount: false,
          },
          display: true,
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
<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
:root {
  --page-width: 750px;
  --font-size: 18px;
}

* {
  font-family: 'Product Sans', Arial, Helvetica, sans-serif;
  user-select: none;
}
body {
  margin: 0;
}
.headerWrapper {
  z-index: 999;
  /*width: 100vw;*/
  width: 100%;
  border-bottom: 2px solid #e8e9ea;
  position: absolute;
  top: 0px;
  background-color: #fbfbfb;
}
.header {
  color: rgba(0, 0, 0, 0.6);
  font-size: 26px;
  padding: 16px 0 16px 0;
  max-width: var(--page-width);
  height: 32px;
  margin: auto;
}
svg {
  width: 28px;
  padding: 3px;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}
svg:hover {
  transform: scale(1.01, 1.01);
  background-color: #f5f5f5;
  border-radius: 20px;
}

.editInput {
  outline: none;
  width: fit-content;
  height: calc(var(--font-size) + 2px);
  font-size: calc(var(--font-size) - 2px);
}
.mainInput {
  font-size: var(--font-size);
  margin: 78px 0 10px 0;
  width: calc(100% - 40px);
  border: 2px solid #e8e9ea;
  border-radius: 30px;
  max-width: var(--page-width);
  padding: 20px;
  transition: all 0.3s ease-in-out;
}
.mainInput:hover {
  box-shadow: 0px 0px 5px 5px #ededed;
}
.mainInput:focus {
  outline: none;
}
.home {
  width: var(--page-width);
  margin: auto;
}

.amountCounter {
  font-size: calc(var(--font-size));
}
.timeStamp {
  height: 15px;
  margin: 0px;
  display: flex;
  font-size: calc(var(--font-size) - 8px);
  align-items: center;
}
.inline {
  padding: 6px;
}
.mainText {
  font-size: var(--font-size);
  margin: auto;
  word-wrap: break-word;
  max-width: 400px;
}

.created-edited {
  justify-content: center;
  align-items: center;
}
.leftWrap,
.rightWrap {
  /*top: 100%;*/
  display: flex;
  justify-content: center;
  align-items: center;
}
.listWrap {
  display: grid;
  grid-template-rows: auto;
  margin-bottom: 80px;
  transition: all 0.3s ease-in-out;
}
.item {
  display: flex;
  justify-content: space-between;
  background-color: white;
  margin-top: 8px;
  padding: 5px;
  border-radius: 30px;
  border: 2px solid #e8e9ea;
}

.item:hover {
  transform: scale(1.01, 1.01);
  box-shadow: 0px 0px 5px 5px #ededed;
}
.footer {
  max-width: var(--page-width);
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: auto;
  height: inherit;
  width: var(--page-width);
}
footer {
  bottom: 0;
  background-color: #fbfbfb;
  height: 50px;
  width: 100%;
  position: fixed;
  border-top: 2px solid #e8e9ea;
  font-weight: 400;
  font-size: 16px;
  color: rgba(0, 0, 0, 0.6);
}

.leftFooter,
.rightFooter {
  height: inherit;
  display: flex;
  align-items: center;
}
.socialMedia {
  width: 30px;
  height: 30px;
}
@media (max-width: 900px) {
  :root {
    --page-width: 400px;
    min-width: 300px;
  }

  .timeStamp {
    display: inline;
    margin-left: 10px;
  }
  .leftWrap,
  .rightWrap {
    /*margin-left: 10px;*/
    padding: 5px;
    justify-content: flex-start;
  }
  .rightWrap {
    border-top: 2px solid #e8e9ea;
    left: 0;
  }
  .amountCounter {
    margin-left: 5px;
  }
  .item {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  }
}
</style>
