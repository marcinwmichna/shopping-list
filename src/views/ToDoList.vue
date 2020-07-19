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
        <div class="leftFooter">
          <div class="aboutMe">
            By
          </div>
          <p class="aboutMe">
            Marcin Michna
          </p>
        </div>

        <div class="rightFooter">
          <p>
            git
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import moment from 'moment';

// import 'bootstrap/dist/css/bootstrap.min.css';

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
  --page-width: 900px;
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
  /*padding-left: 40px;*/
  /*font-size: calc(var(--font-size) + 6px);*/
  max-width: var(--page-width);
  /*width: 100%;*/
  height: 32px;
  /*text-align: center;*/
  margin: auto;
}
/*button {*/
/*  border-radius: 40px;*/
/*  border: none;*/
/*  color: #757575;*/
/*  padding: 5px 10px;*/
/*  text-align: center;*/
/*  text-decoration: none;*/
/*  display: inline-block;*/
/*  font-size: 12px;*/
/*  margin: 2px;*/
/*}*/
.deteleBtn {
  /*padding: 16px;*/
  /*background-color: lightgray;*/
  /*transition: all 0.2s ease-in-out;*/
}
.deteleBtn:hover {
  /*transform: scale(1.01, 1.01);*/
  /*background-color: #f5f5f5;*/
  /*border-radius: 20px;*/
  /*cursor: pointer;*/
  /*fill: red;*/
}

.IncrementBtn {
  background-color: #b5ead7;
}
.IncrementBtn:hover {
  background-color: #bcddd4;
  /*cursor: pointer;*/
}
.IncrementBtn:focus {
  outline-color: #bcddd4;
}
/*box-shadow: red;*/
.DecrementBtn {
  background-color: #ffb3ba;
}
.DecrementBtn:hover {
  background-color: #ff9aa2;
  /*cursor: pointer;*/
}
.DecrementBtn:focus {
  outline-color: #ff9aa2;
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
.amountCounterButtons {
  margin-right: 2px;
  transition: all 0.2s ease-in-out;
}

.editInput {
  outline: none;
  width: fit-content;
  height: calc(var(--font-size) + 2px);
  font-size: calc(var(--font-size) - 2px);
}
.mainInput {
  font-size: var(--font-size);
  /*margin-top: 78px;*/
  /*margin-bottom: 10px;*/
  margin: 78px 0 10px 0;
  width: calc(100% - 40px);
  border: 2px solid #e8e9ea;
  border-radius: 30px;
  max-width: var(--page-width);
  padding: 20px;
  /*border: none;*/
  /*box-shadow: 1px 1px 1px 1px #efefef;*/
  transition: all 0.3s ease-in-out;
}
.mainInput:hover {
  box-shadow: 0px 0px 5px 5px #ededed;
}
.mainInput:focus {
  outline: none;
  /*-moz-outline-radius: 30px;*/
  /*outline: dodgerblue;*/
  /*outline-color: dodgerblue;*/
  /*-moz-outline-radius: 80px;*/
  /*outline: #4d90fe;*/
  /*border: 2px solid #4d90fe;*/
  /*-webkit-box-shadow: 0px 0px 5px #4d90fe;*/
  /*box-shadow: 0px 0px 5px #4d90fe;*/
}
.home {
  height: 100vh;
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
  /*display: inline-block;*/
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
  margin-bottom: 80px;
}
.item {
  display: flex;
  justify-content: space-between;
  background-color: white;
  /*border-radius: 8px;*/
  margin-top: 8px;
  padding: 5px;
  border-radius: 30px;
  border: 2px solid #e8e9ea;
  /*box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);*/
  transition: all 0.3s ease-in-out;
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
  /*margin: auto;*/
  margin: auto;

  width: 100%;
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
  top: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.aboutMe {
  margin-left: 10px;
  /*padding: 10px;*/
}
</style>
