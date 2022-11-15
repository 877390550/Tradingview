<script setup>
import {onMounted } from 'vue'
// 引入tradingview的js
let script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'https://s3.tradingview.com/tv.js';
document.body.appendChild(script);
// 由于tradingview的插件需要指定图表插入的div的id,而id是唯一的，想要复用该组件就必须使用props接收从父组件传过来的div的id
const props = defineProps(['id'])
const Widget=()=>{
    new TradingView.widget(
    {
    "autosize": true,//自动占满父元素
    "symbol": "OKX:BTCUSDT.P",//标的，应设置为可选
    "interval": "1",//时间周期,1为1min
    "timezone": "Asia/Shanghai",//时区
    "theme": "dark",//暗色主题
    "style": "1",//价格展示方式，1为K线图
    "locale": "zh_CN",//语言
    "hidevolume":true,//隐藏成交量
    "percentage":false,//隐藏标题上单根K线详细数据，如开高低收等
    "hide_top_toolbar": true,//隐藏顶部工具栏，指标，时间周期等
    "container_id": 'tradingview_'+props.id
  }
    );
    console.log(props.id)
}

onMounted(() => {
  console.log(`the component is now mounted.`)
  setTimeout(() => {
    Widget()
  }, 3000);
})
</script>

<template>
</template>

<style>
    .comcontainer{
        width: 100%;
        height: 100%;
    }
</style>