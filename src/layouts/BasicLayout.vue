<template>
  <van-nav-bar
      left-arrow
      @click-left="onClickLeft"
      @click-right="onClickRight"
  >
    <template #title>
      <div class="title-container">
        <img src="../assets/Find.svg" class="title-icon" alt="伙伴图标" />
        <span>{{ title }}</span>
      </div>
    </template>

    <template #right>
      <van-icon name="search" size="18"/>
    </template>
  </van-nav-bar>


  <div id="content">
    <router-view/>
  </div>
  <van-tabbar route @change="onChange">
    <van-tabbar-item to="/" name="index"><img src="../assets/Home.svg" class="custom-icon" />主页</van-tabbar-item>
    <van-tabbar-item to="/team"  name="team"><img src="../assets/Check.svg" class="custom-icon" />队伍</van-tabbar-item>
    <van-tabbar-item to="/user"  name="user"><img src="../assets/People.svg" class="custom-icon" />个人</van-tabbar-item>
  </van-tabbar>
</template>

<script setup lang="ts">
import { useRouter } from "vue-router";
import {ref} from "vue";
import routes from "../config/route";

const router = useRouter();
const DEFAULT_TITLE = '伙伴匹配';
const title = ref(DEFAULT_TITLE);

/**
 * 根据路由切换标题
 */
router.beforeEach((to, from) => {
  const toPath = to.path;
  const route = routes.find((route) => {
    return toPath == route.path;
  })
  title.value = route?.title ?? DEFAULT_TITLE;
})

const onClickLeft = () => {
  router.back();
};

const onClickRight = () => {
  router.push('/search')
};

</script>

<style scoped>
#content {
  padding-bottom: 50px;
}

.custom-icon {
  width: 25px;    /* 控制图标宽度 */
  height: 25px;   /* 控制图标高度 */
  margin-right: 6px; /* 图标与文字的间距 */
  vertical-align: middle; /* 垂直对齐文字 */
}

/* 标题容器 */
.title-container {
  display: flex;
  align-items: center;
}

/* 标题图标 */
.title-icon {
  width: 28px;
  height: 28px;
  margin-right: 6px;
  object-fit: contain;
  vertical-align: middle;
}

.van-tabbar-item {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 15px; /* 文字大小 */
  font-weight: bold;
}
</style>
