<template>
    <div class="container">
        <div class="left-container">
            <div class="searchbar-container">
                <SearchBar 
                    @addItemsList="addItems"
                    @filter-list="filterList"
                    @reset-list="resetList"
                    :add-button="addButton"
                    :search-string='searchString'
                />
            </div>
            <div class="list-container">
                <ItemsList
                    ref="ItemsList"
                    :filter-data="filter"
                    :search-string='searchString'  
                />
            </div>
        </div>
        <div class="right-container">
            <div class="sort-container">
                <Sort @sort="callSortItems"/>
            </div>
        </div>
    </div>
</template>

<script>
import { defineComponent, ref } from 'vue';
import SearchBar from './SearchBar.vue';
import ItemsList from './ItemsList.vue';
import Sort from './Sort.vue';
import _ from "lodash";

export default defineComponent({
    name: 'MainPage',
    components: {
        SearchBar,
        ItemsList,
        Sort,
    },
    setup() {
        // Setup
        let filter = ref(null);
        let addButton = ref(false);
        let searchString = ref(null);
        const listItems = ref([
            { item_name: 'Sun', created_at: new Date() },
            { item_name: 'Moon', created_at: new Date() },
            { item_name: 'Star', created_at: new Date() },
        ]);
        return {
            listItems,
            filter,
            addButton,
            searchString,
        }
    },
    created() {
        if(!localStorage.getItem('setItem')){
            window.localStorage.setItem('setItem', JSON.stringify(this.listItems))
        } 
    },
    methods: {
        addItems(){
            let input = document.querySelector('.add-search-input');
            if(input.value.length){
                let items = JSON.parse(localStorage.getItem('setItem'));
                items.push({ item_name: input.value, created_at: new Date() });
                localStorage.setItem('setItem', JSON.stringify(items))
                input.value = '';
                this.$refs.ItemsList.getListItems();
            }
        },
        filterList(value) {
            this.searchString = value;
            let items =  JSON.parse(localStorage.getItem('setItem'));
            this.filter = items.filter( item => _.lowerCase(item.item_name).includes(_.lowerCase(value)) );
            if(this.filter){
                this.match = this.filter.find(item => _.lowerCase(item.item_name)  == _.lowerCase(value));
                this.$refs.ItemsList.sortedlist(this.filter);
                if(this.match){
                    this.addButton = true;
                }else{
                    this.addButton = false;
                }
            }
        },
        resetList() {
            this.filter = null;
            this.searchString = null;
            this.addButton = false;
            this.$refs.ItemsList.getListItems();
        },
        callSortItems(event) {
            this.$refs.ItemsList.getListItems(event.target.value);
        },
    },
});
</script>

<style lang="scss">
.container {
    margin: 0 auto;
    max-width: 1170px;
    padding: 0 15px;
    margin-top: 30px;
    height: 90vh;
    scroll-behavior: smooth;
    overflow-y: scroll;
    .left-container{
        width: 70%;
        float: left;
    }
    .right-container{
        width: 30%;
        float: right;
        margin-top: 90px;
        padding: 0 50px;
    }
}
</style>