<template>
  <div class="progress-container">
    <div style="margin-bottom: 20px">
      <van-circle
        v-model:current-rate="currentRate"
        layer-color="#ebedf0"
        :rate="percentage"
        :text="
          status === 'unknown' ? '未知' : status === 'normal' ? '正常' : '报警'
        "
      >
        <div class="progress-content">
          <i class="iconfont icon-info"></i>
          <span>{{ percentage }}%</span>
          <div class="progress-text">{{ getText(percentage) }}</div>
        </div>
      </van-circle>
    </div>

    <van-slider v-model="percentage" :max="100" />

    <footer>
      <img
        :src="getImg(percentage)"
        alt=""
        class="footerImg"
        style="width: 50px; height: 50px; margin-right: 10px"
      />
      <aside style="display: flex; flex-direction: column">
        <span>检测状态：</span> <span>{{ getText(percentage) }}</span>
      </aside>
    </footer>
  </div>
</template>

<script setup>
import { defineComponent, ref, computed } from "vue";
import { ElProgress, ElSlider } from "element-plus";

const percentage = ref(0);

const status = computed(() => {
  if (percentage.value === 0) {
    return "unknown";
  } else if (percentage.value <= 50) {
    return "success";
  } else {
    return "warning";
  }
});

const getText = (percentage) => {
  if (percentage === 0) {
    return "未知";
  } else if (percentage <= 50) {
    return "正常";
  } else {
    return "报警";
  }
};

const getImg = (percentage) => {
  if (percentage === 0) {
    return "https://i.postimg.cc/LX4xkxVw/weizhi-3x.png";
  } else if (percentage <= 50) {
    return "https://i.postimg.cc/K8FpvcMm/zhengchang-3x.png";
  } else {
    return "https://i.postimg.cc/NfWGV8n9/baojing-3x.png";
  }
};
</script>

<style scoped>
.progress-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.custom-content {
  display: flex;
  justify-content: space-around;
  align-items: center;
  font-size: 24px;
  color: #1989fa;
}

.progress-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.progress-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.iconfont {
  font-size: 80px;
  margin-bottom: 10px;
  color: #409eff;
}

.progress-text {
  font-size: 24px;
  font-weight: bold;
}
footer {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-top: 20px;
}
</style>
