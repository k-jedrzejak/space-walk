<template>
    <div class="hero-image"></div>
</template>

<script>

export default({
    name: "HeroImage"
})

</script>

<style lang="less" scoped>

@layer-color: #466c6e;

.hero-image {
    background-image: url("../assets/bg.jpg");
    background-size: cover;
    background-position: center;
    position: absolute;
    top:0;
    right: 0;
    bottom: 0;
    left: 0;

    &:after {
        content: '';
        background:  @layer-color;
        position: absolute;
        top:0;
        right: 0;
        bottom: 0;
        left: 0;
        opacity: .45;
    }
}

</style>