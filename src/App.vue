<template>
  <headercomponent @home-view="viewhome" @list-view="viewlist" :wishlist="wishlist"/>

  <cardcomponent :visible="wishisvisible" :books="books" :wishlist="wishlist" @addToList="addToList"/>

  <wishlistcomponent :wishlist="wishlist" :visible="wishisvisible" @removeFromList="removeFromList"/>
  
</template>

<script>
import {booksData} from "./assets/books"
import headercomponent from "./components/headercomponent.vue"
import cardcomponent from "./components/cardcomponent.vue"
import wishlistcomponent from "./components/wishlistcomponent.vue"
export default {
  name: "App",
  components: {
    headercomponent,
    cardcomponent,
    wishlistcomponent
  },
  data: () => ({
    targetcomponent:'wishlistcomponent',
    message: "hello world",
    books: booksData,
    wishisvisible: false,
    wishlist: [],
  }),
  methods: {
    viewhome(){
      this.wishisvisible = false;
    },
    viewlist(){
      this.wishisvisible = true;
    },
    addToList(book) {
      this.wishlist.push(book);
    },
    disableAddBtn(book) {
      return this.wishlist.some((item) => item.ISBN === book.ISBN);
    },
    removeFromList(book) {
      let bookIndex = this.wishlist.indexOf(book);
      this.wishlist.splice(bookIndex, 1);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
