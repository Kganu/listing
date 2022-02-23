<template>
    <span class="check-icon">
    </span>
</template>

<script>
export default {
    name: 'Check',
    setup() {
        return
    },
}
</script>

<style lang="scss">
@import "../sass/_color.scss";
.check-icon {
    width: 24px;
    height: 24px;
    position: relative;

    &:after {
    content: '';
    position: absolute;
    width: 24px;
    height: 24px;
    background-image: url(/img/check.074f15c9.svg);
    background-repeat: no-repeat;
    left: 5px;
    }
}
</style>