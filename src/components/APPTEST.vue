<script setup>
import{ref} from 'vue'
import Tradingview from './Tradingview.vue'
// 引入tradingview的js
let script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'https://s3.tradingview.com/tv.js';
document.body.appendChild(script);
//品种列表
const tableData = [
  {
    symbol: 'BTCUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'ETHUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'ENSUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'FILUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'UNIUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'MATICUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'APEUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'AAVEUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'SOLUSDT.P',
    source: 'OKX',
  },
  {
    symbol: 'LTCUSDT.P',
    source: 'OKX',
  },
  
]

let testlist=[]
for(let i=0;i<tableData.length/3;i++){
  testlist[i]={
    row:i,
    symbolist:[{
      id:i*3,
      ...tableData[i*3],
    },
    {
      id:i*3+1,
      ...tableData[i*3+1],
    },
    {
      id:i*3+2,
      ...tableData[i*3+2],
    },
  ]
  }
}
//你首先应该知道为什么要这么设计列表的结构，因为要在模板渲染时使用row来渲染行，再在每一行里面渲染该行包含的三个数据，v-for需要知道数组的索引和值或者知道对象的索引和键值对才能渲染
// 处理后的列表结构应该为：
// testlist:[
//   {row:0,
//     symbollist:[{id:0,name:'btc',soruce:'okx'},{...},{...}]
//   },
//   {row:1,
//     symbollist:[{id:0,name:'btc',soruce:'okx'},{...},{...}]
//   },
//   {row:2,
//     symbollist:[{id:0,name:'btc',soruce:'okx'},{...},{...}]
//   },
// ]

let config = ref({ //config的数据仅在dialog中修改,不传输到子组件
  list: tableData,
  locale: "zh_CN",//语言
  hide_top_toolbar: true,//隐藏顶部工具栏，指标，时间周期等
  hide_side_toolbar: true,//绘图工具栏
  hidevolume: true,//隐藏成交量
  theme: 'dark',//暗色主题
  interval: "5",//时间周期,1为1min
  timezone: "Asia/Shanghai",//时区
})
let post = { ...config.value } //传递的参数不应该响应式，否则不按确认就马上触发onUpdated

const handleCurrentChange = (val) => {
  console.log(`current page: ${val}`)
}
const currentPage = ref(1)
</script>

<template>
  <div class="container">
    <div class="layoutcontainer" > 
  <el-row v-if="!configVisible" v-for="(value,index) in testlist" :key="index"  v-show="(currentPage-1)===parseInt(value.row/3)">
    <el-col :span="8" v-for="(item,index) in value.symbolist" :key="index">
      <Tradingview v-bind="post" :id=item.id />
   </el-col>
  </el-row>
  <el-pagination layout="prev, pager, next" :total="testlist.length"  :page-size='3' @current-change="handleCurrentChange"   v-model:current-page="currentPage"/>
</div>

  </div>

</template>

<style lang="less">
.container {

  .layoutcontainer{
  height: 100vh;
  display: flex;
  flex-direction: column;
  .el-row{
    flex: 1;
    margin-bottom: 0;
    .grid-content {
      height: 100%;
}
  }
  
  }
}

.example-pagination-block + .example-pagination-block {
  margin-top: 10px;
}


* {
  margin: 0;
  padding: 0;
  overflow: hidden;
}
</style>
