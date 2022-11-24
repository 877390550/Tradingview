<script setup>
import { ref} from 'vue'
import {
  Minus,
  Menu as IconMenu,
  Grid,
} from '@element-plus/icons-vue'
import Tradingview from './components/Tradingview.vue'
// 引入tradingview的js
let script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'https://s3.tradingview.com/tv.js';
document.body.appendChild(script);
//-----分屏设置-------
let mode = ref(4)
const handleSwitch = (val) => {
  mode.value = Number(val.index);
}
//-----分屏设置-------
// -----全局配置---------
//品种列表
const tableData = [
  {
    sid: 1,
    symbol: 'BTCUSDT.P',
    source: 'OKX',
  },
  {
    sid: 2,
    symbol: 'ETHUSDT.P',
    source: 'OKX',
  },
  {
    sid: 3,
    symbol: 'ENSUSDT.P',
    source: 'OKX',
  },
  {
    sid: 4,
    symbol: 'FILUSDT.P',
    source: 'OKX',
  },
  {
    sid: 5,
    symbol: 'UNIUSDT.P',
    source: 'OKX',
  },
  {
    sid: 6,
    symbol: 'MATICUSDT.P',
    source: 'OKX',
  },
  {
    sid: 7,
    symbol: 'APEUSDT.P',
    source: 'OKX',
  },
  {
    sid: 8,
    symbol: 'AAVEUSDT.P',
    source: 'OKX',
  },
  {
    sid: 9,
    symbol: 'SOLUSDT.P',
    source: 'OKX',
  },
]
let configVisible = ref(false)
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
const handleConfig = () => {
  configVisible.value = true
}
const handleSubmit = () => {
  post = ref({ ...config.value })
  configVisible.value = false
}
// -----全局配置---------
// --------test-----------
const test = () => {
}
// --------test-----------

</script>

<template>
  <div class="container">
    <!-- table -->
    <!-- 全局配置弹窗 -->
    <el-dialog v-model="configVisible" title="全局配置" @click="test">
      <!-- 品种列表 -->
      <el-table :data="tableData" height="250">
        <el-table-column prop="symbol" label="商品代码" />
        <el-table-column prop="source" label="来源" />
        <el-table-column fixed="right" label="操作">
          <template #default>
            <el-button link type="primary" size="small">修改</el-button>
            <el-button link type="primary" size="small">删除</el-button>
            <el-button link type="primary" size="small">置顶</el-button>
          </template>
        </el-table-column>
      </el-table>
      <!-- 品种列表 -->
      <!-- 下方选项区 -->
      <el-row :gutter="20">
        <el-col :span="8">
          <div class="grid-content ep-bg-purple-light">
          </div>
        </el-col>
        <el-col :span="8">
          <div class="grid-content ep-bg-purple-light">
          </div>
        </el-col>
        <el-col :span="8">
          <div class="grid-content ep-bg-purple"></div>
        </el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="8">
          <el-form class="grid-content ep-bg-purple">
            <el-form-item label="语言" :label-width="0">
              <el-select v-model="config.locale">
                <el-option label="中文" value="zh_CN" />
                <el-option label="英文" value="en" />
              </el-select>
            </el-form-item>
          </el-form>
        </el-col>
        <el-col :span="8">
          <el-form class="grid-content ep-bg-purple-light">
            <el-form-item label="主题颜色" :label-width="0">
              <el-select v-model="config.theme">
                <el-option label="暗色" value="dark" />
                <el-option label="亮色" value="light" />
              </el-select>
            </el-form-item>
          </el-form>
        </el-col>
        <el-col :span="8">
          <el-checkbox v-model="config.hide_top_toolbar" label="隐藏顶部工具栏" size="large"
            class="grid-content ep-bg-purple" />
        </el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="8">
          <el-form class="grid-content ep-bg-purple">
            <el-form-item label="时区" :label-width="0">
              <el-select v-model="config.timezone">
                <el-option label="UTC-10" value="Pacific/Honolulu" />
                <el-option label="UTC-9" value="America/Juneau" />
                <el-option label="UTC-8" value="America/Los_Angeles" />
                <el-option label="UTC-7" value="US/Mountain" />
                <el-option label="UTC-6" value="America/Mexico_City" />
                <el-option label="UTC-5" value="America/Bogota" />
                <el-option label="UTC-4" value="America/Caracas" />
                <el-option label="UTC-3" value="America/Sao_Paulo" />
                <el-option label="UTC+0" value="Europe/Dublin" />
                <el-option label="UTC+1" value="Europe/Paris" />
                <el-option label="UTC+2" value="Africa/Cairo" />
                <el-option label="UTC+3" value="Asia/Bahrain" />
                <el-option label="UTC+3:30" value="Asia/Tehran" />
                <el-option label="UTC+4" value="Asia/Dubai" />
                <el-option label="UTC+5" value="Asia/Karachi" />
                <el-option label="UTC+5:30" value="Asia/Kolkata" />
                <el-option label="UTC+5:45" value="Asia/Kathmandu" />
                <el-option label="UTC+6" value="Asia/Almaty" />
                <el-option label="UTC+7" value="Asia/Bangkok" />
                <el-option label="UTC+8" value="Asia/Shanghai" />
                <el-option label="UTC+9" value="Asia/Tokyo" />
                <el-option label="UTC+10" value="Australia/Brisbane" />
                <el-option label="UTC+10:30" value="Australia/Adelaide" />
                <el-option label="UTC+11" value="Australia/Sydney" />
                <el-option label="UTC+12" value="Pacific/Norfolk" />
                <el-option label="UTC+13" value="Pacific/Auckland" />
                <el-option label="UTC+13:45" value="Pacific/Chatham" />
              </el-select>
            </el-form-item>
          </el-form>
        </el-col>
        <el-col :span="8">
          <el-form class="grid-content ep-bg-purple-light">
            <el-form-item label="时间周期" :label-width="0">
              <el-select v-model="config.interval">
                <el-option label="1分钟" value="1" />
                <el-option label="3分钟" value="3" />
                <el-option label="5分钟" value="5" />
                <el-option label="15分钟" value="15" />
                <el-option label="30分钟" value="30" />
                <el-option label="1小时" value="60" />
                <el-option label="2小时" value="120" />
                <el-option label="3小时" value="180" />
                <el-option label="4小时" value="240" />
                <el-option label="1天" value="D" />
                <el-option label="1周" value="W" />
              </el-select>
            </el-form-item>
          </el-form>
        </el-col>
        <el-col :span="8">
          <el-checkbox v-model="config.hidevolume" label="隐藏成交量" size="large" class="grid-content ep-bg-purple" />
        </el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="8">
          <div class="grid-content ep-bg-purple-light">
          </div>
        </el-col>
        <el-col :span="8">
          <div class="grid-content ep-bg-purple-light">
          </div>
        </el-col>
        <el-col :span="8">
          <el-checkbox v-model="config.hide_side_toolbar" label="隐藏绘图工具" size="large"
            class="grid-content ep-bg-purple" />
        </el-col>
      </el-row>
      <!-- 下方选项区 -->
      <template #footer>
        <span class="dialog-footer">
          <el-button type="primary" @click="handleSubmit">
            确认并重置图表
          </el-button>
        </span>
      </template>
    </el-dialog>
    <!-- 全局配置弹窗 -->
    <!-- 导航 -->
    <div class="menu">
      <el-menu default-active="4" class="el-menu-vertical-demo" collapse mode='horizontal'>
        <el-menu-item @click="handleConfig">
          <el-icon>
            <Grid />
          </el-icon>
          <template #title>全局配置</template>
        </el-menu-item>
        <el-menu-item index="1" @click="handleSwitch">
          <el-icon>
            <Minus />
          </el-icon>
          <template #title>二分</template>
        </el-menu-item>
        <el-menu-item index="2" @click="handleSwitch">
          <el-icon>
            <icon-menu />
          </el-icon>
          <template #title>四分</template>
        </el-menu-item>
        <el-menu-item index="3" @click="handleSwitch">
          <el-icon>
            <Grid />
          </el-icon>
          <template #title>九分</template>
        </el-menu-item>
      </el-menu>
    </div>
    <!-- 导航 -->
    <!-- 原始布局 -->
    <!-- <table class="tablecontainer">
      <tr>
        <td>
          <Tradingview id='0' v-bind="post" />
        </td>
        <td v-show="mode > 1">
          <Tradingview id='1' v-bind="post" />
        </td>
        <td v-show="mode > 3">
          <Tradingview id='4' v-bind="post" />
        </td>
      </tr>
      <tr v-show="mode > 2">
        <td v-show="mode > 2">
          <Tradingview id='3' v-bind="post" />
        </td>
        <td v-show="mode > 2">
          <Tradingview id='2' v-bind="post" />
        </td>
        <td v-show="mode > 3">
          <Tradingview id='5' v-bind="post" />
        </td>
      </tr>
      <tr v-show="mode > 3">
        <td v-show="mode > 3">
          <Tradingview id='6' v-bind="post" />
        </td>
        <td v-show="mode > 3">
          <Tradingview id='7' v-bind="post" />
        </td>
        <td v-show="mode > 3">
          <Tradingview id='8' v-bind="post" />
        </td>
      </tr>
    </table> -->
    <!-- 原始布局 -->
    <!-- el布局 -->
    <!-- 默认模板监听el-row,只修改el-col是不会触发视图更新的 -->
    <div class="layoutcontainer" > 
    <el-row v-if="!configVisible">
    <el-col :span="8" class="TVbox">
      <Tradingview id='0' v-bind="post" />
   </el-col>
   <el-col :span="8" class="TVbox">
      <Tradingview id='1' v-bind="post" />
   </el-col>
   <el-col :span="8" class="TVbox">
      <Tradingview id='2' v-bind="post" />
   </el-col>
  </el-row>
  <el-row v-if="!configVisible">
    <el-col :span="8" class="TVbox">
      <Tradingview id='3' v-bind="post" />
   </el-col>
   <el-col :span="8" class="TVbox">
      <Tradingview id='4' v-bind="post" />
   </el-col>
   <el-col :span="8" class="TVbox">
      <Tradingview id='5' v-bind="post" />
   </el-col>
  </el-row>
  <el-row v-if="!configVisible">
    <el-col :span="8" class="TVbox">
      <Tradingview id='6' v-bind="post" />
   </el-col>
   <el-col :span="8" class="TVbox">
      <Tradingview id='7' v-bind="post" />
   </el-col>
   <el-col :span="8" class="TVbox">
      <Tradingview id='8' v-bind="post" />
   </el-col>
  </el-row>
</div>
    <!-- el布局 -->
  </div>
</template>

<style lang="less">
.container {
  // el布局
.tablecontainer{
  width: 100%;
  height: 100%;
}
  // el布局

  .layoutcontainer{
  height: 100vh;
  display: flex;
  flex-direction: column;
  .el-row{
    flex: 1;//el-row是layoutcontainer容器中的子元素，该容器垂直排列，设置flex:1使其垂直方向铺满容器
    margin-bottom: 0;
    .grid-content {
      height: 100%;
}
  }
  
  }

  .menu {
    width: 50px;
    position: absolute;
    z-index: 999;
    opacity: 0.3;
    bottom: 0;
    left: 0;
  }

  .el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 100%;
    height: 100px;
  }
}

.el-menu--collapse {
  width: calc(var(--el-mDenu-icon-width) + var(--el-menu-base-level-padding) * 3);
  height: 30px;
}

.el-row {//dialog配置中的elrow
  margin-bottom: 20px;
}

.el-row:last-child {
  margin-bottom: 0;
}

.el-col {
  border-radius: 4px;
}

.grid-content {
  border-radius: 4px;
  min-height: 36px;
}


* {
  margin: 0;
  padding: 0;
  overflow: hidden;
}
</style>
