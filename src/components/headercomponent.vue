<template>
        <nav class="navbar bg-dark">
            <div class="container-fluid d-flex align-items-baseline">
              <a class="navbar-brand" href="#" @click.prevent="viewhome">Home Page</a>
              <p class="navbar-brand fs-3" style="color:white;margin-left:px;">Welcome To Our Book Store</p>
                <a class="navbar-brand bg-primary text-light px-3 rounded-3" href="#" @click.prevent="viewlist">
                  Wish List [{{wishlist.length}}] {{wishlist.length == 1 ? 'book' : 'books'}}
                </a>
            </div>
        </nav>
</template>

<script>
export default {
    data(){
        return{
        }
    },
    methods:{
        viewhome(){
            this.$emit("home-view");
        },
        viewlist(){
            this.$emit("list-view");
        }
    },
    props:["wishlist"]
}
</script>