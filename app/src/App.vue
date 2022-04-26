<template>
  <div class="container">
    <v-header 
    @set-search='getSearch'
    :get-product-count="dataProductCount">
    </v-header>
    <div>
      <sort-price
      @set-sort-price='getSortPrice'
      ></sort-price>
    </div>
    <div class="row row-cols-4">
      <one-card 
        v-for="(item, index) in showProduct" 
        :key="index"
        :one-product="item"
        @get-count-product='postCountProduct'>
        </one-card>
    
    </div>
  
    
    
  </div>
  
  
</template>

<script>
import VHeader from './components/VHeader.vue'
import OneCard from './components/OneCard.vue'
import  SortPrice  from './components/SortPrice.vue'

let url = './json/product.json';
export default {
  name: 'App',
  components: {
    VHeader,
    OneCard,
    SortPrice
    
    
    
  },
  data() {
    return {
      dataProduct: [],
      dataProductCount:[],
      seartchText:'',
      sortStr: ''
    }
  },
  computed:{
    showProduct(){
      let output = [...this.dataProduct];
        if (this.seartchText) {
          output = output.filter(i=> `${i.title + ' ' + i.price +' ' + i.category +' ' + i.description}`
                              .toLowerCase()
                              .includes(this.seartchText));
        }
        if (this.sortStr) {
          if (this.sortStr == 'Up') {
            console.log('Up');
            return output.sort((a,b)=> a.price - b.price);
          }
          if(this.sortStr == 'Down'){
            console.log('Down');
            return output.sort((a,b)=> b.price - a.price);
          }
      }
      


      return output;
    }
  },

  methods:{
      postCountProduct(objInfoCount){
          this.dataProductCount.push(objInfoCount)
         //console.log(this.dataProductCount);
            
      },
      getSearch(search){
        this.seartchText = search;
        //console.log(search);
      },
      getSortPrice(valueSort){
        this.sortStr = valueSort;
        //console.log(valueSort);
      }
  },
   async mounted(){
        let data = await fetch(url);
            data = await data.json()
            console.log(data);
        this.dataProduct = data;
        
    }



}
</script>







<style>
*{
  box-sizing: border-box;
  font-family: 'Plus Jakarta Sans', sans-serif;
}



</style>
