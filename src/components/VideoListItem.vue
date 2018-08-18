<template>
    <li class="list-group-item media" @click="onVideoSelect">
        <img class="mr-3" :src="thumbnailUrl" />
        <div class="media-body">
            {{ aVideo.snippet.title}}
        </div>
    </li>
</template>

<script>
export default {
    name: 'VideoListItem',
    props: ['aVideo'],
    computed: {
        thumbnailUrl() {
            return this.aVideo.snippet.thumbnails.default.url;
        }
    },
    methods: {
        onVideoSelect() {
            this.$emit('videoSelect', this.aVideo);
        }
    }
}
</script>

<style scoped>
    li {
        display: flex;
        cursor: pointer;
    }

    li:hover {
        background-color: #eeeeee
    }
</style>
