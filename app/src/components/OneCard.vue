<template>
    <div class=" my-card p-3">
            <div class="product-id text-end">
                <p> 
                    Код:{{showProduct.id}}
                </p>

            </div>
            <div class="card-img">
                <img :src="showProduct.image" alt="">
            </div>
            <div class="product-info">
                <div class="product-info-title px-2"> 
                    <h5>{{showProduct.title}}

                    </h5>
                </div>
                <div class="product-category">
                    <h6 class="ps-3 pt-3"> Category: {{showProduct.category}}</h6>
                </div>
                <div class="product-info-description ps-3 pt-2 text-start"> 
                
                </div>
                
                <div class="">
                    <div class="text-center py-3 inputPrice d-flex justify-content-around">
                        <div class="product-price">
                            <span class="fs-4 fw-bold">{{showProduct.price}} $</span>
                        </div>
                        <div class="d-flex align-items-center">
                            
                            <input 
                            v-model="count"
                            class="" 
                            type="number" 
                            min=1>
                            <button 
                            @click="getCountProduct"
                            class="ms-2 btn btn-success"
                            ><i class="fa-solid fa-basket-shopping"></i></button>
                            
                            
                        </div>
                    </div>
                </div>
            </div>
        </div>
</template>


<script>
export default {
    name:'OneCard',
    data() {
        return {
            count: 1,
            arrCount:[]
            
        }
    },
    props:['oneProduct'],
    computed:{
        showProduct(){
           return this.$props.oneProduct;
        }
    },
    methods:{
         getCountProduct(){
                let output = {count: this.count,
                                id:this.showProduct.id,
                                summPrice: this.showProduct.price * this.count}
                 
                // console.log(this.arrCount);
                return this.$emit('get-count-product',output)  
            
        }
    }
    
}
</script>


<style scored>
.my-card{
  position: relative;
  transition: 0.1s;
  border-radius: 25px;
  display: flex;
  flex-direction: column;
  border: 1px solid #ffffff;
  transition: 0.5s;
}
.my-card:hover{
  border: 1px solid #dadada;
}
.card-img{
  width: 100%;
  
  margin: auto;
  text-align: center;
}
.card-img img{
  
  width: 200px;
  height: 300px;
  object-fit: contain;
  transition: 0.2s;
}
.card-img img:hover{
  transform: scale(1.05);
  
  
}
.product-info-title{
  text-align: center;
  
}
.inputPrice input{
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: bold;
  width: 50px;
  height: 38px;
}
</style>