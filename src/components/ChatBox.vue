<template>
  <div class="chat">
    <div class="chatItem">
        <div v-for="(item, index) in list" :key="index" :class="{'item': true, 'active':item.active}" @click="selectItem(item)" >
            <div class="left">
                <img :src="item.imgSrc" alt="">
            </div>
            <div class="right">
                <p class="title">{{item.name}}</p>
                <p class="info">{{item.newInfo}}</p>
            </div>
        </div>
    </div>
    <div class="itemRoom">
      <div class="title">{{currenItem.roomName}}</div>
      <div class="mailContent">{{currenItem.infos}}</div>
      <div class="tool"></div>
      <div class="mailInput">
        <a-textarea placeholder="Basic usage" :autosize="{ minRows: 5, maxRows: 5 }" />
        <a-button class="sendBtn" type="primary">发送</a-button>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
export default {
    name: 'Chat',
    data() {
        return {
            active: false,
            list: [
                {name: '22', imgSrc:'https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png', newInfo: 'hello!', infos: [1,2,3,4,5,6,7]},
                {name: '33', imgSrc:'https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png', newInfo: 'hello!'},
                {name: '44', imgSrc:'https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png', newInfo: 'hello!'},
                {name: '55', imgSrc:'https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png', newInfo: 'hello!'},
                {name: '66', imgSrc:'https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png', newInfo: 'hello!'},
            ],
            currenItem: { roomName:'', infos: []}
        }
    },
    methods: {
        selectItem(item) {
            this.currenItem.roomName = item.name;
            this.currenItem.infos = item.infos;
            this.$nextTick(function() {
                this.list.forEach(item => {
                    this.$set(item, 'active', false);
                })
                this.$set(item, 'active', true);
            })
        }
    },
    mounted() {
        this.currenItem.roomName = this.list[0].name;
        this.currenItem.infos = this.list[0].infos;
        this.$set(this.list[0], 'active', true);
    }
}
</script>

<style >
.chat {
  width: 100%;
  height: 100%;
}
.chat .chatItem {
  width: 30%;
  height: 100%;
  float: left;
}
.chat .chatItem .item{
    position: relative;
    margin: 5px;
    border: 1px solid black;
    width: 95%;
    height: 60px;
    background-color: white;
}
.chat .chatItem .item:hover{
    background-color:slategrey;
}
.chat .chatItem .active{
    background-color: #6e6e6e;
}
.chat .chatItem .item .left{
    position: absolute;
    float: left;
    width: 30%;
}
.chat .chatItem .item .left img{
    width:48px;
    height: 48px;
}
.chat .chatItem .item .right{
    float: right;
    width: 70%;
    text-align: left;
    font-weight: bold;
}
.chat .chatItem .item .right .title{
    margin: 0;
    padding-top: 10px;
}
.chat .chatItem .item .right .info{
    margin: 0;
    /* padding-bottom: 10px; */
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
.chat .itemRoom {
  width: 70%;
  height: 100%;
  float: left;
  background-color: aqua;
}
.chat .itemRoom .title {
  height: 5%;
  background-color: yellow;
}
.chat .itemRoom .mailContent {
  height: 65%;
}
.chat .itemRoom .tool {
  height: 5%;
  background-color: chocolate;
}
.chat .itemRoom .mailInput {
  height: 25%;
  background-color: aliceblue;
  position: relative;
}
.chat .itemRoom .mailInput .sendBtn {
  position: absolute;
  right: 20px;
  bottom: 2px;
}
</style>