<template>
        <div v-if="visible">
            <div v-if="wishlist.length == 0" class="fs-2 my-3" style="color:red;text-align:center;">There is no books in your wish list , please add books first</div>
            <div v-if="wishlist.length > 0" >
                <table class="table table-striped text-center mt-2">
                    <thead>
                        <tr>
                            <th>Title</th>
                            <th>Author</th>
                            <th>No of pages</th>
                            <th>Price</th>
                            <th>Remove</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="book in wishlist" :key="book.ISBN">
                            <td>{{book.title}}</td>
                            <td>{{book.author}}</td>
                            <td>{{book.noOfPages}}</td>
                            <td>{{formatCurrency(book.price.value)}}</td>
                            <td><button class="btn btn-danger" @click="removeFromList(book)">Delete</button></td>
                        </tr>
                    </tbody>
                    <tfoot>
                        <tr style="width:100%;font-weight: bold;">
                            <td colspan="2">Total Price</td>
                            <td colspan="3">{{formatCurrency(getTotalPrice())}}</td>
                        </tr>
                    </tfoot>
                </table>
            </div>
        </div>
</template>

<script>
export default {
    data(){
        return {

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
        getTotalPrice() {
            let totalPrice = 0;
            for (let i = 0; i < this.wishlist.length; i++) {
                totalPrice += this.wishlist[i].price.value;
            }
            return totalPrice;
        },
        removeFromList(book){
            this.$emit("removeFromList",book);
        }
    },
    props:["wishlist","visible"]
}
</script>