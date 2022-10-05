<script setup lang="ts">
import { onMounted, ref } from "vue";
import { YoutubeVue3 } from "youtube-vue3";
interface Video {
  name: string;
  id: string;
  ytUrl: string;
  creators: [string];
  docId: string;
}

const youtube = ref();
const video_time = ref();
const video = ref<Video>({
  name: "",
  ytUrl: "",
  id: "",
  docId: "",
  creators: [""],
});

// eslint-disable-next-line @typescript-eslint/no-unused-vars
async function goToVideoTime(time: number) {
  youtube.value.player.pauseVideo();
  await youtube.value.player.seekTo(time, true);
}
async function VIDEO() {
  const v = 'https://www.youtube.com/watch?v=GE_8MURePbo';
  // const v = 'https://www.youtube.com/watch?v=GE_8MURePbo';
  // const v = await firebase.getVideo(props.videoId);
  const Video: Video = {
    name: 'demo',
    ytUrl: 'www.youtube.com/watch?v=GE_8MURePbo',
    id: 'GE_8MURePbo',
    docId: 'GE_8MURePbo',
    creators: '',
    // name: v.data()?.name,
    // ytUrl: v.data()?.ytUrl,
    // id: v.data()?.id,
    // docId: v.id,
    // creators: v.data()?.creators,
  };
  return Video;
}

function playCurrentVideo() {
  youtube.value.player.playVideo();
}
function stopCurrentVideo() {
  youtube.value.player.stopVideo();
}
async function pauseCurrentVideo() {
  youtube.value.player.pauseVideo();
  video_time.value = await youtube.value.player.getCurrentTime();
}
function onEnded() {
  console.log("## OnEnded")
}
function onPaused() {
  console.log("## OnPaused")
}
function onPlayed() {
  console.log("## OnPlayed")
}

onMounted(async () => {
  video.value = await VIDEO()
})
</script>

<template>
  <div>
    <h1>About OLS</h1>
    <p>
      OLS, the Open Learning Server, is about bringing education to technology.
    </p>
    <hr>
    <h3>Video</h3>
    <h6>{{ video.name }}</h6>
    <YoutubeVue3 :videoid="video.id" ref="youtube" :width="960" :height="640" @ended="onEnded" @paused="onPaused"
      @played="onPlayed" />
    <hr />
    <br>
    <input v-model="video.id" />
    <hr />
    <br>
    {{ video.id }}
    <button @click="applyConfig">Apply</button>
    <button @click="playCurrentVideo">Play</button>
    <button @click="stopCurrentVideo">Stop</button>
    <button @click="pauseCurrentVideo">Pause</button>
    <hr />
    {{ video_time }}
  </div>
</template>