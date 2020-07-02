<template>
    <div class="container">
        <div class="list" id="list" ref="list" >
            <ul>
                <li v-for="(item,index) in msglist" :key="index">
                    <RightItem :id="item.id" :type="item.type" :content="item.content" v-if="item.me"></RightItem>
                    <LeftItem :id="item.id" :type="item.type" :content="item.content" v-else></LeftItem>
                    <div v-scroll style="height: 0"></div>
                </li>
            </ul>
        </div>
        <div class="bottom">
            <div class="line"></div>
            <div class="input-send">
                <van-field v-model="text" placeholder="请输入聊天内容..." class="input" @keyup.enter="send"/>
                <van-button plain type="info" class="send" @click="send">发送</van-button>
            </div>

        </div>

    </div>
</template>

<script>
    import Vue from "vue";
    import {getChatResponse} from "@/api/ApiChat";
    import LeftItem from "@/components/LeftItem";
    import RightItem from "@/components/RightItem";

    Vue.directive('scroll', {
        inserted(el) {
            el.scrollIntoView()
        }
    })

    export default {
        name: "Chat",
        components: {LeftItem, RightItem},
        data: () => {
            return {
                text: '',
                msglist: [{
                    id: 1,
                    type: 1,
                    content: '欢迎你！',
                    me: false
                }]
            }
        },
        methods: {
            send() {
                if (this.text) {
                    this.msglist.push({
                        id: this.msglist[this.msglist.length - 1].id + 1,
                        type: 1,
                        content: this.text,
                        me: true
                    })
                    if (this.text === '图片') {
                        this.msglist.push({
                            id: this.msglist[this.msglist.length - 1].id + 1,
                            type: 2,
                            content: 'http://6emm.hxzdhn.com/img/2020/06/28/jausoellbtf.jpg',
                            me: false
                        })
                    } else {
                        this.getResponse(this.text)
                    }
                    this.text = ''
                }
            },
            getResponse(text) {
                getChatResponse(text).then(res => {
                    console.log(res)
                    this.msglist.push({
                        id: this.msglist[this.msglist.length - 1].id + 1,
                        type: 1,
                        content: res.data.answer,
                        me: false
                    })
                })
            }
        }
    }
</script>

<style scoped lang="scss">
    .container {
        ul {
            padding: 0;
            margin: 0;
        }

        li {
            list-style: none;

        }

        .list {
            width: 100%;
            height: 100%;
            margin-bottom: 45px;
        }

        .bottom {
            width: 100%;
            position: fixed;
            bottom: 0;

            .line {
                width: 100%;
                height: 1px;
                background-color: #ddd;
            }

            .input-send {
                display: flex;
                justify-content: space-between;
                background-color: #fff;

                .input {
                    padding-right: 10px;
                }

                .send {
                    width: 80px;
                    height: 30px;
                    margin-top: 7px;
                    margin-right: 10px;
                }
            }

        }
    }


</style>