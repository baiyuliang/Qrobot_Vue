<template>
    <div class="container">
        <img class="head"
             src="https://dss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1068485212,3292662520&fm=111&gp=0.jpg"/>
        <div class="content">
            <div class="text" v-if="type===1" style="word-break: break-all;">
                {{content}}
            </div>
            <img class="img" :src="content" v-else-if="type===2"/>
        </div>
    </div>
</template>

<script>

    export default {
        name: "RightItem",
        props: ['id', 'type', 'content']
    }
</script>

<style scoped lang="scss">
    .container {
        display: flex;
        padding: 10px 15px;
        margin-left: 60px;
        flex-direction: row-reverse;

        .head {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: 1px solid #eee;
        }

        .content {
            margin-right: 10px;
            margin-top: 10px;

            .text {
                background-color: #eee;
                border-bottom-left-radius: 10px;
                padding: 5px 5px;
                font-size: 14px;
                color: #000;
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