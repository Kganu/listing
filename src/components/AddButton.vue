<template>
    <span class="add-btn">
        <img class="add" @click="$emit('handleAdd')" src="../assets/add.svg" />
    </span>
</template>

<script>
export default {
    name: 'AddButton',
    setup() {
        return
    },
}
</script>

<style lang="scss">
@import "../sass/_color.scss";
.add-btn {
    position: absolute;
    top: 1px;
    right: 0;
    padding: 3px 8px 0 8px;
    line-height: 17px;
    cursor: pointer;
    background: $cyan-blue;
}
</style>