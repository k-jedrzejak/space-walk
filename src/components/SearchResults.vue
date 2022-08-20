<template>
    <div class="image-box" :style="style"></div>
</template>

<script>

export default({
    name: 'SearchResults',
    props: {
            item: {
        type: Object,
        required: true
    }
    },

    data() {
        return {
            photo: this.item.links[0].href,
        };
    },
    computed: {
        style() {
            return `background-image: url("${this.photo}")`;
        },
    }
   
})
</script>


<style lang="less">

.image-box {
    width: 300px;
    height: 300px;
    background-position: center;
}

</style>
