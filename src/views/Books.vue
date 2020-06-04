<template>
  <div class="book-container">
    <h1>My Books</h1>
     <book :book="book" v-for="book in mybooks" :key="book.id" />
  </div>
</template>

<script lang="ts">
    import { Component, Vue } from "vue-property-decorator";
    import IBook from '../types/Books';
    import BooksService from '@/services/books-service';
    import Book from '@/components/Book.vue';

    const bookService = new BooksService()

    @Component({
        name: 'MyBooks',
        components:{ Book }
    })
    export default class MyBooks extends Vue{
        //data
        mybooks:IBook[] = [];

        //computed properties
        get bookCount(){
            return this.mybooks.length;
        }
        //prop
        //methods
        //lifecycle hooks
        created(){
           bookService.getAllBooks().then(res => this.mybooks = res)
           .catch(err => console.error(err))
        }
        //watchers
    }
</script>

<style lang="scss">
</style>