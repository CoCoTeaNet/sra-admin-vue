<template>
  <el-container style="height: 100vh;">
    <el-aside width="300">
      <NavMenu style="height: 100%;overflow: auto"/>
    </el-aside>

    <el-container>
      <el-header class="layout-box-shadow"><admin-header/></el-header>

      <el-main>
        <router-view v-slot="{Component}">
          <keep-alive>
            <transition :name="`slide-fade`" :mode="`out-in`">
              <component :is="Component"/>
            </transition>
          </keep-alive>
        </router-view>
      </el-main>

    </el-container>
  </el-container>
</template>

<script setup lang="ts">
import NavMenu from "./modules/NavMenu.vue";
import AdminHeader from "./modules/AdminHeader.vue";
</script>

<!--私有样式-->
<style scoped>
/* 可以设置不同的进入和离开动画 */
/* 设置持续时间和动画函数 */
.slide-fade-enter-active {
  transition: all .6s ease;
}

.slide-fade-leave-active {
  transition: all .3s cubic-bezier(0.42, 0, 0.58, 1);
}

.slide-fade-enter, .slide-fade-leave-to {
  transform: translateX(74px);
  opacity: 0;
}
</style>

<style>
.layout-box-shadow {
  border-bottom: 1px solid var(--el-border-color);
  box-shadow: var(--el-box-shadow-light);
}
</style>
