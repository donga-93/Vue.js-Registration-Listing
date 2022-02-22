<template>
<div>
 <h2>Product List</h2>
 <ul class="item" v-for="item in list" :key="item.id">
    <div class="card1">
    <img :src="item.image" alt="Avatar" style="width:50%">
    <div class="container1">
    <h4><span style="color:blue;font-weight:bold">Categorty</span> : {{item.category}}</h4> 
    <h4><span style="color:lime;font-weight:bold">Description</span> : {{item.description}}</h4> 
    <h4><span style="color:red;font-weight:bold">Price</span> : {{item.price}}</h4> 
    <h4><span style="color:goldenrod;font-weight:bold">Rating</span> : {{item.rating.rate}}</h4> 
    <h4><span style="color:magenta;font-weight:bold">Title</span> : {{item.title}}</h4> 
  </div>
</div>

    </ul>
 </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios'
Vue.use(VueAxios,axios)
export default {
    name: "App",
    data()
    {
        return {
            list: []
        }
    },
  async  mounted() 
    {
        let result = await axios.get("https://fakestoreapi.com/products");
        console.warn(result.data);
        this.list = result.data
    }
}
</script>

<style>
 .card1 {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 40%;
  float: left;
  padding: 10px;
  margin: 30px;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container1 {
  float: center;
}

</style>