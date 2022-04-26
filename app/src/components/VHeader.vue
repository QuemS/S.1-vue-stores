<template>
    <div class="pt-4 ">
        <nav class="navbar navbar-expand-lg navbar-light bg-light ">
            <div class="container-fluid d-flex ">
                
                    <div 
                    class=" px-4 py-3 collapse navbar-collapse justify-content-between VheaderNavBar" 
                    id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                            <a class="navbar-brand" href="#">Navbar</a>
                        <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Categories</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Profile</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Contact</a>
                        </li>
                   </ul>
                    <form  class="form-inline my-2 my-lg-0 d-flex searchNavBar">
                        <input  
                        v-model="searchText"
                        class="form-control mr-sm-2" 
                        type="search" 
                        placeholder="Search" 
                        aria-label="Search">
        
                    </form>
                    <div class="buttonCard ms-2">
                        <button class=" py-2 px-2  btn btn-success d-flex justify-content-around">
                        <span class="numberCard" :data-number="showCount"><i class="fa-solid fa-basket-shopping"></i></span>
                        <span v-if="showPrice">{{showPrice}}</span>
                        <span v-else>Cart</span>
                        
                        
                        </button>
                     </div>
                </div>
            </div>
        </nav>
   </div>
</template>

<script>
export default {
    name: 'VHeader',
    data(){
        return{
            title:'Hello VHeader',
            countArr: [],
            searchText: ''
        }
    },
    props:['getProductCount'],
    computed:{
        showPrice(){
            if (this.countArr.length >= 1) {
                let output = this.countArr.reduce((acc,item)=> acc+ item.summPrice,0);
                console.log(output);
                return Math.round(output *100)/100 + '$';
            }
            return '';
        },
        showCount(){
            if (this.countArr.length >= 1) {
                let output = this.countArr.reduce((acc,item)=> acc+ item.count,0);
                console.log(output);
                return output;
            }
            return '';
        }

    },
    watch:{
        searchText(newSearch){
            return this.$emit('set-search',newSearch)
        }
    },
    methods:{
       
        
        
           
    
    },
    created(){
        this.countArr = this.$props.getProductCount;
    }
}
</script>


<style scored>
.VheaderNavBar{
    background-color: #2d835b;
    border-radius: 10px;
}
.buttonCard button{
    width: 150px;
}
.buttonCard button span{
  position: relative;
   
}
.numberCard::after{
    content: attr(data-number);
    position: absolute;
    top: -85%;
    left: 55%;
    font-size: 1rem;
    height: auto;
    width: auto;
    background-color: orange;
    border-radius: 14px;
    text-align: center;
    padding: 0px 8px;
}
.searchNavBar input{
  min-width: 600px;
}
</style>