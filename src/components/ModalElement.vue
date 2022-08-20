<template>

<div class="modal">
    <div class="close-btn" @click="$emit('closeModal')">close</div>

    <div class="modal-content">
        <div class="modal-image">
            <img :src="photo" alt="">
        </div>
        <div class="modal-info">
            <div class="title">Title: {{title}}</div>
            <div class="desc">Description: {{desc}}</div>
            <div class="author">Author: {{author}}</div>
            <div class="date">Date: {{date}}</div>
        </div>
    </div>
   
</div>
    
</template>

<script>
export default {
    name: "ModalElement",
    props: ['item'],
      data() {
        return {
            photo: null,
            title: null,
            desc: null,
            author: null,
            date: null
        }
    },
    mounted() {
        this.photo = this.item.links[0].href
        this.title = this.item.data[0].title
        this.desc = this.item.data[0].description.substring(0,150)
        this.author = this.item.data[0].secondary_creator
        this.date = this.item.data[0].date_created
        console.log(this.item.data[0])
    }
}

</script>

<style lang="less" scoped>
.modal {
    position: fixed;
    top: 50%;
    transform: translate(0, -50%);
    max-width: 80%;
    z-index: 2;
    background: #fff;
    padding: 30px;
    border: 1px solid lightblue;
    width: 80%;
    height:80%;

    .modal-content {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;

        .modal-image {
            width: 60%;
            height: 100%;
            margin-right: 24px;

            img {
                max-width: 100%;
                max-height: 100%;
            }
        }

        .modal-info {
            width: 40%;
        }
    }

    .close-btn {
        position: absolute;
        right: 20px;
        top: 20px;
    }
}
</style>