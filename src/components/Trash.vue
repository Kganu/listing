<template>
    <span>
        <img class="trash" @click="$emit('deleteNode', itemName)"  src="../assets/trash.svg" />
    </span>
</template>

<script>
export default {
    name: 'Trash',
    props: {
        itemName: String,
    },
    setup() {
        return
    },
}
</script>

<style>

</style>