<script setup>
import { ref } from 'vue'
import {
  Minus,
  FullScreen,
  Menu as IconMenu,
  Grid,
} from '@element-plus/icons-vue'
import Tradingview from './components/Tradingview.vue'
let mode = ref(1)
const handleSwitch = (val) => {
  mode.value = Number(val.index);
}

</script>

<template>
  <div class="container">

    <!-- table -->
    <table class="table">
      <!-- 导航 -->
      <div class="menu">
        <el-menu default-active="1" class="el-menu-vertical-demo" collapse mode='horizontal'>
          <el-menu-item index="1" @click="handleSwitch">
            <el-icon>
              <FullScreen />
            </el-icon>
            <template #title>满屏</template>
          </el-menu-item>
          <el-menu-item index="2" @click="handleSwitch">
            <el-icon>
              <Minus />
            </el-icon>
            <template #title>二分</template>
          </el-menu-item>
          <el-menu-item index="3" @click="handleSwitch">
            <el-icon>
              <icon-menu />
            </el-icon>
            <template #title>四分</template>
          </el-menu-item>
          <el-menu-item index="4" @click="handleSwitch">
            <el-icon>
              <Grid />
            </el-icon>
            <template #title>九分</template>
          </el-menu-item>
        </el-menu>
      </div>
      <!-- 导航 -->
      <!-- 变换布局 -->
      <tr>
        <td><div id="tradingview_1" class="td">
          <Tradingview id='1'/>
        </div>
        </td>
        <td v-show="mode > 1" ><div id="tradingview_2" class="td">
          <Tradingview id='2'/>
        </div>
        </td>
        <td v-show="mode > 3"><div id="tradingview_3" class="td">
          <Tradingview id='3'/>
        </div></td>
      </tr>
      <tr v-show="mode > 2">
        <td v-show="mode > 2"><div id="tradingview_4" class="td">
          <Tradingview id='4'/>
        </div></td>
        <td v-show="mode > 2"><div id="tradingview_5" class="td">
          <Tradingview id='5'/>
        </div></td>
        <td v-show="mode > 3"><div id="tradingview_6" class="td">
          <Tradingview id='6'/>
        </div></td>
      </tr>
      <tr v-show="mode > 3">
        <td v-show="mode > 3"><div id="tradingview_7" class="td">
          <Tradingview id='7'/>
        </div></td>
        <td v-show="mode > 3"><div id="tradingview_8" class="td">
          <Tradingview id='8'/>
        </div></td>
        <td v-show="mode > 3"><div id="tradingview_9" class="td">
          <Tradingview id='9'/>
        </div></td>
      </tr>
      <!-- 变换布局 -->
    </table>
    <!-- table -->
  </div>
</template>

<style lang="less">



.container {
  height: 100vh;
.menu{
  position: absolute;
}
  .table {
    width: 100%;
    height: 100%;

    td{
      text-align: center;
      vertical-align: middle;
    }

    .td{
      width: 100%;
      height: 100%;
    }

  }

  .el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 100%;
    position: absolute;
  }
}

body {
  margin: 0;
}
</style>
