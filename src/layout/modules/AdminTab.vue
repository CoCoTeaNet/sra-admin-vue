<template>
  <div style="display: flex">
    <el-scrollbar>
      <div class="scrollbar-flex-content">
        <p v-for="item in menuStore.tabItems" :key="item" :class="`scrollbar-tab-item ${item.isActive?'active':''}`">
          <span @click="onClick(item)">{{ item.name }}</span>
          <el-icon class="tab-icon" @click="menuStore.removeTabItem(item.id)">
            <close/>
          </el-icon>
        </p>
      </div>
    </el-scrollbar>
    <el-dropdown>
        <span class="el-dropdown-link">
          <el-icon class="el-icon--right">
            <arrow-down/>
          </el-icon>
        </span>
      <template #dropdown>
        <el-dropdown-menu>
          <el-dropdown-item @click="refresh">刷新页面</el-dropdown-item>
          <el-dropdown-item @click="onCloseAll">关闭所有</el-dropdown-item>
        </el-dropdown-menu>
      </template>
    </el-dropdown>
  </div>
</template>

<script lang="ts" setup>
import {ArrowDown, Close} from "@element-plus/icons-vue";
import {router} from "@/router";
import {useRoute} from "vue-router";
import {onMounted} from "vue";
import {useMenuStore} from "@/stores/menu.ts";

const menuStore = useMenuStore();
const route = useRoute();

onMounted(() => {
  menuStore.addTabItem({name: JSON.parse(JSON.stringify(route.meta)).title, url: route.path, isActive: true});
});

const onClick = (obj: any) => {
  router.push({path: obj.url});
  menuStore.tabItems.forEach((item: TabItem) => {
    item.isActive = item.id == obj.id;
  });
}

const onCloseAll = () => {
  menuStore.initTabItems();
}

const refresh = () => {
  window.location.reload();
}
</script>

<style scoped>
.scrollbar-flex-content {
  display: flex;
}

.tab-icon {
  margin-left: 1px;
  padding: 1px;
  /* 过渡效果设置 */
  transition: all 0.3s ease-in-out;
}

.tab-icon:hover {
  border-radius: 16px;
  color: var(--el-color-primary);
  background-color: var(--el-color-white);
}

.scrollbar-tab-item {
  font-size: 12px;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 23px;
  margin: 3px;
  padding: 0 0.8em;
  text-align: center;
  background: var(--el-color-white);
  border: 1px solid var(--el-border-color);
  border-radius: 3px;
  color: var(--el-button-text-color);
  /* 过渡效果设置 */
  transition: all 0.3s ease-in-out;
}

.scrollbar-tab-item:hover {
  cursor: pointer;
}

.active {
  background-color: var(--el-color-primary);
  color: var(--el-color-white);
}

.el-dropdown-link {
  cursor: pointer;
  color: var(--el-color-primary);
  display: flex;
  align-items: center;
}
</style>
