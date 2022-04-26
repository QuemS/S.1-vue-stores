<template>
    <div class="text-end py-3">
        <select class="custom-select custom-select-sm"
        @click="gerSort($event.target.selectedOptions[0].value)"
        >
            <option>Sort</option>
            <option value="Up" >Price Up</option>
            <option value="Down">Price Down</option>
         </select>
    </div>
</template>
<script>
export default {
    name:'SortPrice',
    methods:{
        gerSort(value){
            return this.$emit('set-sort-price',value)
        }
    }
}
</script>
<style scored>
    
</style>