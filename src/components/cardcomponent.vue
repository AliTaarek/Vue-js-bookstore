<template>
    <div v-if="!visible" class="d-flex flex-wrap justify-content-around">
            <div v-for="book in books" :key="book.ISBN" class="card m-2 p-2" :class="[book.noOfPages > 50 ? 'more' :'less']" style="width: 16rem;">
                <img :src="book.image" class="card-img-top" alt="book image">
                <div class="card-body row justify-content-between py-3 align-items-center">
                  <div class="bg-info text-center my-1 p-1 rounded-3">Author : {{book.author}}</div>
                  <div class="bg-info text-center my-1 p-1 rounded-3">Category : {{book.title}}</div>
                  <div class="bg-danger text-center col-5 p-1 rounded-3">{{book.noOfPages}} pages</div>
                  <div class="bg-warning text-center my-1 col-5 p-1 rounded-3 fs-5">{{formatCurrency(book.price.value)}}</div>
                  <div class="bg-success text-center my-1 p-1 rounded-3">ISBN: {{book.ISBN}}</div>
                  <button class="btn btn-primary" @click="addToList(book)" :disabled="disableAddBtn(book)">Add To WishList</button>
                </div>
            </div>
    </div>
</template>

<script>
export default {
    data(){
        return{

        }
    },
    methods:{
        formatCurrency(value) {
            let formatter = Intl.NumberFormat("ar-SA", {
                style: "currency",
                currency: "SAR",
                maximumFractionDigits: 1,
            }).format(value);
            return formatter;
        },
        addToList(book){
            this.$emit("addToList",book);
        },
        disableAddBtn(book) {
             return this.wishlist.some((item) => item.ISBN === book.ISBN);
        }
    
    },
    props:["visible","books","wishlist"]
}
</script>
<style scoped>
     .more{
            background-image:linear-gradient(to bottom,transparent 30%,lightblue)
        }
    .less{
            background-image:linear-gradient(to bottom,transparent 30%,lightyellow)
        }
</style>