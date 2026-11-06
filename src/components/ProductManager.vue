<script setup>
import { getProducts, createProduct, deleteProducts } from '../api/products';


</script>

<script>
    export default{
        name: "ProductManager",
        data(){
            return{
                products: [],
                newProduct: {
                    name: "",
                    price: 0,
                    inStock: false,
                }
            }

                
            
        },
        methods: {
            async loadProducts(){
                this.products = await getProducts();
            },
            async addProduct(product){
                await createProduct(product);
                await this.loadProducts();
            },
            async submitCreateProduct(){
                await this.addProduct(this.newProduct);
            },
            async removeProducts(id){
                await deleteProducts(id);
                await this.loadProducts();
            },
        },
        mounted() {
            this.loadProducts();
        }
    }
</script>

<template>
    <main class="">termekek</main>
    <table class="flex flex-col w-full">
        <thead class="w-full p-2">
            <tr class="flex justify-around gap-8">
            <th>id</th>
            <th>name</th>
            <th>price</th>
            <th>in stock</th>
        </tr></thead>
        <tbody class="w-full">
            <tr v-for="product in products" class="flex justify-around gap-8">
                <td class="">{{ product.id }}</td>
                <td class="">{{ product.name }}</td>
                <td class="">{{ product.price }}</td>
                <td class="">{{ product.inStock ? 'Igen' : 'Nem' }}</td>
                <td class="">
                    <button type="button" @click="removeProducts(product.id)">Torles</button>
                </td>
            </tr>
        </tbody>
        
    </table>
    <form class="mt-30 flex flex-col border-2   " @submit.prevent="submitCreateProduct">
        <label for="name">Nev</label>
        <input type="text" name="name"  v-model="this.newProduct.name"/><br>
        <label for="price">Ar</label>
        <input type="number" name="price" v-model="this.newProduct.price"/>
        <label for="inStock">Instock</label>
        <input type="checkbox" name="inStock" v-model="this.newProduct.inStock"><br>
        <button type="submit">Letrhozas</button>
    </form>
</template>