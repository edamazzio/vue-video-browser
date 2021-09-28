<template>
  <ul class="list-group col-md-4">
    <VideoListItem
        v-for="video in videos"
        :video="video"
        :key="video.etag"
        @videoSelect="onVideoSelect"
    >

    </VideoListItem>
  </ul>
</template>

<script>
import VideoListItem from "@/components/VideoListItem";
export default {
  name: "VideoList",
  components: {VideoListItem},
  methods: {
    onVideoSelect(video){
      this.$emit("videoSelect", video)
    }
  },
  props: {
    videos: Array,
  }
}
</script>

<style scoped>

</style>