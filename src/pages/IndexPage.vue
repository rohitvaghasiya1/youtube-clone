<template>
  <q-page>
    <div class="video-wrapper row">
      <VideoCard v-for="(item, index) in videos" :key="index" :video="item" />
    </div>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
import VideoCard from "../components/VideoCard.vue";
defineOptions({
  name: "IndexPage",
});
const videos = ref([
  {
    title: "Video 1",
    subtitle: "video subtitle 1",
    views: "112 views",
    banner: "https://cdn.quasar.dev/img/parallax1.jpg",
    user: { name: "Joi doe", avatar: "" },
  },
  {
    title: "Video 2",
    subtitle: "video subtitle 2",
    views: "11 views",
    banner: "https://cdn.quasar.dev/img/parallax2.jpg",
    user: { name: "Joi doe", avatar: "" },
  },
  {
    title: "Video 3",
    subtitle: "video subtitle 3",
    views: "112 views",
    banner: "https://cdn.quasar.dev/img/mountains.jpg",
    user: { name: "Joi doe", avatar: "" },
  },
  {
    title: "Video 4",
    subtitle: "video subtitle 1",
    views: "112 views",
    banner: "https://cdn.quasar.dev/img/quasar.jpg",
    user: { name: "Joi doe", avatar: "" },
  },
  {
    title: "Video 1",
    subtitle: "video subtitle 1",
    views: "112 views",
    banner: "https://cdn.quasar.dev/img/parallax1.jpg",
    user: { name: "Joi doe", avatar: "" },
  },
  {
    title: "Video 2",
    subtitle: "video subtitle 2",
    views: "11 views",
    banner: "https://cdn.quasar.dev/img/parallax2.jpg",
    user: { name: "Joi doe", avatar: "" },
  },
  {
    title: "Video 3",
    subtitle: "video subtitle 3",
    views: "112 views",
    banner: "https://cdn.quasar.dev/img/mountains.jpg",
    user: { name: "Joi doe", avatar: "" },
  },
  {
    title: "Video 4",
    subtitle: "video subtitle 1",
    views: "112 views",
    banner: "https://cdn.quasar.dev/img/quasar.jpg",
    user: { name: "Joi doe", avatar: "" },
  },
]);
</script>
<style lang="scss">
.video-wrapper {
  padding: 20px 10px;
  flex-wrap: wrap;
}
</style>
