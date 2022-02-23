<template>
    <div>
        <div class="radio-outer">
            <label for="item_name">Sort by value</label>
            <input id="item_name" type="radio" name="sortBy" value="item_name" checked="checked" @change="$emit('sort', $event)" /> 
        </div>
        <div class="radio-outer">
            <label for="created_at">Sort by added date</label>
            <input id="created_at" type="radio" name="sortBy" value="created_at" @change="$emit('sort', $event)" />
        </div>
    </div>
</template>

<script>
export default {
    name: 'Sort',
    setup() {
        return
    },
}
</script>

<style lang="scss">
    @import "../sass/_color.scss";
    .radio-outer{
        padding: 10px 30px;
        cursor: pointer;
        border-bottom: 1px solid $light-grey;
        label{
            cursor: pointer;
        }
        input[type="radio"]{
            cursor: pointer;
            float: right;
        }
    }

</style>