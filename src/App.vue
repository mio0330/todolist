<template>
  <div id="app">
    <div class="top">
      <h2>todolist</h2>
      <input type="text" class="nav" v-model="something" />
      <button class="go" @click="add">添加</button>
    </div>
    <div class="content">
      <div class="doing">
        <h3>
          正在进行中
          <div class="n">{{ n }}</div>
        </h3>
        <ul>
          <li
            v-for="(item, index) in doingList"
            :key="index"
            style="list-style: none; margin: 5px; display: flex"
          >
            <button @click="clear(item)" style="width: 75px">已完成</button>
            <span
              style="
                display: flex;
                flex: 1;
                justify-content: center;
                white-space: nowrap;
              "
              >{{ item.title }}</span
            >
            <button @click="deleteItem(item)" style="width: 50px">删除</button>
          </li>
        </ul>
      </div>
      <div class="doing">
        <h3>
          已完成
          <div class="n">{{ m }}</div>
        </h3>
        <ul>
          <li
            v-for="(item, index) in doneList"
            :key="index"
            style="list-style: none; margin: 5px; display: flex"
          >
            <button @click="again(item)" style="width: 75px">未完成</button>
            <span style="display: flex; flex: 1; justify-content: center">{{
              item.title
            }}</span>
            <button @click="deleteItemtwo(item)" style="width: 50px">
              删除
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      something: "",
      n: 0,
      m: 0,
      doList: [],
      doItem: {
        title: "",
        done: false,
      },
    };
  },
  computed: {
    doingList() {
      return this.doList.filter((item) => {
        return !item.done;
      });
    },
    doneList() {
      return this.doList.filter((item) => {
        return item.done;
      });
    },
  },
  methods: {
    add() {
      this.doList.push({
        title: this.something,
        done: false,
      });
      this.n++;
    },
    clear(item) {
      item.done = true;
      this.n--;
      this.m++;
    },
    again(item) {
      item.done = false;
      this.n++;
      this.m--;
    },
    deleteItem(item) {
      let index = this.doList.indexOf(item);
      this.doList.splice(index, 1);
      this.n--;
    },
    deleteItemtwo(item) {
      let index = this.doList.indexOf(item);
      this.doList.splice(index, 1);
      this.m--;
    },
  },
};
</script>

<style lang="less">
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.top {
  height: 60px;
  width: 100%;
  background: pink;
  border: 1px, solid red;
  display: flex;
  justify-content: center;
  align-items: center;
}
.nav {
  border-radius: 5px;
  height: 25px;
  width: 300px;
  margin: 30px;
}
.go {
  height: 25px;
  width: 50px;
  border: none;
  background: #0282b9;
  border-radius: 4px;
  color: white;
  font-size: 16px;
}
.content {
  width: 40%;
  margin: auto;
}
.n {
  width: 25px;
  height: 25px;
  line-height: 25px;
  background: red;
  border-radius: 50%;
  display: inline-block;
  float: right;
  text-align: center;
  color: white;
}
</style>
