<template>
  <div class="container">
    <!--
      custom listener on SearchBar, 'termChange',
      called within child component using $emit('termChange' ...) 
     -->
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail :video="selectedVideo" />
      <!--
        bind parent data ("videos") and pass it into the child as a prop;
        child accesses prop using name of bound variable (theVideos)
      -->    
      <VideoList @videoSelect="onVideoSelect" :theVideos="someVideos"></VideoList>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = "AIzaSyCMJEZxLbtbRJ7RmTd8_vFLd_5UABg7_kk";

export default {
  name: 'App',
  components: {
    SearchBar: SearchBar,
    VideoList: VideoList,
    VideoDetail
  },
  data: function() {
    return {
      someVideos: [],
      selectedVideo: null
    };
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
    onTermChange(searchTerm) {
      axios
        .get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm
          }
      }).then(response => {
        this.someVideos = response.data.items;
      });
    }
  }
};

</script>

<style>

</style>
