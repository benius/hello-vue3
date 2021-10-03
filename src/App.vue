<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <!-- HelloWorld -->
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <!-- RecursiveTree -->
  <div>
    <recursive-tree :title="bookData.name" :children="bookData.childNodes"></recursive-tree>
  </div>

  <!-- UpdateWithEvent -->
  <div>
    <ul v-for="(book) in books" class="book" :key="book.id">
      <li>{{ book.name }}</li>
      <li>{{ book.author }}</li>
      <li>{{ book.publishedAt }}</li>
    </ul>

    <hr>

    <!-- 直接將 v-for 的 book 物件作為 props 傳遞 -->
    <!-- 並監聽自訂的 update 事件 -->
    <update-with-event v-for="(book, idx) in books" :key="idx" v-bind="book" @update="updateInfo"></update-with-event>
  </div>

  <!-- UpdateWithModel -->
  <div>
    <h1>{{ modelMessage }}</h1>

    <update-with-model v-model="modelMessage"></update-with-model>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import RecursiveTree from "@/components/RecursiveTree";
import UpdateWithEvent from "@/components/UpdateWithEvent";
import UpdateWithModel from "@/components/UpdateWithModel";

export default {
  name: 'App',

  components: {
    UpdateWithModel,
    UpdateWithEvent,
    HelloWorld,
    RecursiveTree
  },

  data() {
    return {
      modelMessage: String,
      bookData: {},
      books: []
    }
  },

  methods: {
    loadBookData() {
      this.bookData = {
        name: '好書推薦',
        childNodes: [{
          name: 'Git',
          url: null,
          childNodes: [{
            name: '為你自己學 Git',
            url: 'https://www.tenlong.com.tw/products/9789864342662'
          }]
        },
          {
            name: '前端開發',
            url: null,
            childNodes: [{
              name: '金魚都能懂的 CSS 選取器',
              url: 'https://www.tenlong.com.tw/products/9789864344994'
            },
              {
                name: '0 陷阱！0 誤解！8 天重新認識 JavaScript！',
                url: 'https://www.tenlong.com.tw/products/9789864344130'
              },
              {
                name: '讓 TypeScript 成為你全端開發的 ACE！',
                url: 'https://www.tenlong.com.tw/products/9789864344895'
              },
            ]
          },
          {
            name: 'IoT',
            url: null,
            childNodes: [{
              name: 'IoT沒那麼難！新手用 JavaScript 入門做自己的玩具！',
              url: 'https://www.tenlong.com.tw/products/9789864345328'
            }]
          },
          {
            name: 'Chatbot',
            url: null,
            childNodes: [{
              name: '人人可作卡米狗：從零打造自己的 LINE 聊天機器人',
              url: 'https://www.tenlong.com.tw/products/9789864342938'
            }]
          }
        ]
      }
    },

    loadBooks() {
      this.books = [
        {
          id: '0001',
          name: '0 陷阱！0 誤解！8 天重新認識 JavaScript！',
          author: 'Kuro Hsu',
          publishedAt: '2019/09'
        },
        {
          id: '0002',
          name: '重新認識 Vue.js',
          author: 'Kuro Hsu',
          publishedAt: '2021/02'
        }
      ]
    },

    updateInfo(val) {
      const idx = this.books.findIndex(d => d.id === val.id);
      this.books[idx] = val;
    },

    prepareModelMessage(val) {
      this.modelMessage = val;
    }
  },

  mounted() {
    this.$nextTick(function () {
      this.loadBookData()
      this.loadBooks()
      this.prepareModelMessage('Try installing the bundle "GetBundles".')
    })

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
