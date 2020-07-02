<template>
    <div class="container">
        <img class="head" src="https://pp.myapp.com/ma_icon/0/icon_42284557_1517984341/96"/>

        <div class="content">
            <div class="text" v-if="type===1">
                {{content}}
            </div>
            <img class="img" :src="content" v-else-if="type===2" @click="preview(content)"/>
        </div>

    </div>
</template>

<script>
    import ImagePreview from "vant/lib/image-preview";

    export default {
        name: "LeftItem",
        props: ['id', 'type', 'content'],
        methods: {
            preview(url){
                ImagePreview([url])
            }
        }
    }
</script>

<style scoped lang="scss">
    .container {
        display: flex;
        padding: 10px 15px;
        margin-right: 60px;

        .head {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: 1px solid #eee;
        }

        .content {
            margin-left: 10px;
            margin-top: 10px;

            .text {
                background-color: deepskyblue;
                border-bottom-right-radius: 10px;
                padding: 5px 5px;
                font-size: 14px;
                color: #fff;
            }

            .img {
                width: 100px;
                border-bottom-right-radius: 10px;
                border-top-right-radius: 10px;
                border-bottom-left-radius: 10px;
            }
        }

    }
</style>