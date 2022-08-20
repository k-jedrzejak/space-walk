<template>
    <div class="logo-container">
        <div class="logo">Space•Walk</div>
    </div>

</template>

<script>

export default {
    name: "LogoImage"
}

</script>


<style lang="less" scoped>

@text-color: #fff;
@shadow-color: #01595c;

 .logo-container {
    text-align: center;
    position: absolute;
    top:20px;
    left: 50%;
    transform: translate(-50%);

    .logo {
        color: @text-color;
        text-shadow: 2px 2px 18px @shadow-color;
        font-size: 46px;
        font-weight: bold;
        text-transform: uppercase;
        letter-spacing: 3px;
        margin-bottom: 40px;

        @media (min-width: 768px) {
            font-size: 54px;
        }
    }}
 
</style>