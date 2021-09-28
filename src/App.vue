<template>
  <div id="app" class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail :video="selectedVideo"/>
      <VideoList :videos="videos" @videoSelect="onVideoSelect"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from "@/components/SearchBar";
import VideoList from "@/components/VideoList";
import VideoDetail from "@/components/VideoDetail";

const API_KEY = 'AIzaSyCX9gxl3HXO9ntIJ_F2DsV2RJlVfLDhmyA';
const YOUTUBE_API_URL = 'https://www.googleapis.com/youtube/v3/search';

function onTermChange(searchTerm) {
  axios.get(YOUTUBE_API_URL, {
    params: {
      key: API_KEY,
      type: 'video',
      part: 'snippet',
      q: searchTerm
    }
  }).then(result => {
    this.videos = result.data.items;
  }).catch(err => {
    console.error(err);
  })
}

function onVideoSelect(video) {
  this.selectedVideo = video;
}

export default {
  name: 'App',
  data() {
    return {
      videos: [],
      selectedVideo: null
    }
  },
  components: {
    VideoDetail,
    VideoList,
    SearchBar,
  },
  methods: {
    onTermChange,
    onVideoSelect
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
