<template>
    <div class="claim-container">
        <h1 class="title">{{title}}</h1>
        <div class="sentence">{{sentence}}</div>
        <div class="subsentence">{{subsentence}}</div>
    </div>   
</template>

<script>
    export default({
        name: "HeroClaim",
        props: [
            'title',
            'sentence',
            'subsentence'
        ]

    })
</script>

<style lang="less" scoped>

@text-color: #fff;
@shadow-color: #133738;


    .claim-container {
        text-align: center;
        color: @text-color;
        text-shadow: 4px 4px 6px @shadow-color;

        .title {
            font-size: 46px;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin-bottom: 40px;

            @media (min-width: 768px) {
                font-size: 54px;
            }
        }

        .sentence {
            font-size: 20px;
            margin-bottom:24px;

            @media (min-width: 768px) {
                font-size: 24px;
            }
        }
    }

</style>
