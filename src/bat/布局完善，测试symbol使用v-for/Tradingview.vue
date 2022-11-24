<script setup>
import {onUpdated,toRaw,onBeforeMount,watch} from 'vue'
// 由于tradingview的插件需要指定图表插入的div的id,而id是唯一的，想要复用该组件就必须使用props接收从父组件传过来的div的id
const props = defineProps(['id','locale','hide_top_toolbar','hidevolume','theme','interval','timezone','hide_side_toolbar','list',])
const rawHtml="<div class='compcontainer' id='tradingview_"+props.id+"' ></div>"//利用v-html在组件中生成对应id的div
const symbollist=toRaw(toRaw(props.list))
const Widget=()=>{
    new TradingView.widget(
    {
    // 默认配置,不在设更改交互
    "autosize": true,//自动占满父元素
    "container_id": 'tradingview_'+props.id,
    "style": "1",//价格展示方式，1为K线图
    // 全局配置,应统一监听使界面更新
    "symbol": `${symbollist[props.id].source}:${symbollist[props.id].symbol}`,
    ...toRaw(props),
  }
    );
}
onBeforeMount(() => {
  console.log('onBeforeMount')
  console.log(toRaw(props))

  setTimeout(() => {
    Widget()
  }, 2000);
})
onUpdated(()=>{
  console.log('onUpdated')
  Widget()
})


const handleclick=()=>{
  console.log(props)
}
</script>

<template>
  <div class="outside" @click="handleclick">
    <!-- 原本这个v-html写在一个div里面,结果渲染后比预期的代码多了一个外层div,导致tradingview的container_id父元素宽高设置出错,使用span,span是行内元素,对它设置宽高是无效的,它的宽高由子元素撑开. -->
    <!-- 另外,在备份组件文件时对文件重命名,编辑器会提示是否重构,重构会对根组件app里引用的子组件名称一并修改,最终导致错误引用,如果使用备份,则应该跳过更改. -->
    <span v-html='rawHtml' ></span>
  </div>
</template>

<style>
.compcontainer{
  width: 100%;
  height: 100%;
}
.outside{
  width: 100%;
  height: 100%;
}
</style>