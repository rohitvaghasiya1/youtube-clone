<template>
  <div class="video-card">
    <q-card flat>
      <img :src="video.banner" />
      <q-item class="video-card-content">
        <q-item-section avatar top>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar2.jpg" />
          </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label>{{ video.title }}</q-item-label>
          <q-item-label caption>{{ video.subtitle }}</q-item-label>
          <q-item-label caption>{{ video.views }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-card>
  </div>
</template>

<script setup>
import { ref } from "vue";
defineOptions({
  name: "VideoCard",
});

const props = defineProps({
  video: {
    type: Object,
    required: true,
  },
});
</script>
<style lang="scss" scoped>
.video-card {
  width: 25%;
  padding: 0 10px 20px;
  @media screen and (max-width: $breakpoint-md) {
    width: 33.33%;
  }
  @media screen and (max-width: $breakpoint-sm) {
    width: 50%;
  }
  @media screen and (max-width: $breakpoint-xs) {
    width: 100%;
  }
  .q-card {
    border-radius: 15px;
    @media screen and (max-width: $breakpoint-md) {
      border-radius: 8px;
    }
    img {
      height: 220px;
      object-fit: cover;
      border-radius: 15px;
      @media screen and (max-width: $breakpoint-md) {
        height: 190px;
        border-radius: 8px;
      }
    }
    .video-card-content {
      padding: 20px 0 0;
    }
  }
}
</style>
