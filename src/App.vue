<template>
  <div id="main">
    <VideoCall class="video-call" :roomUrl="roomUrl" />
  </div>
</template>

<script>
import { ref } from "vue";
import VideoCall from "./components/VideoCall.vue";

export default {
  name: "App",
  components: {
    VideoCall,
  },
  setup() {
    const roomUrl = ref("https://chiragkanani.daily.co/U4imlEsWmdYaUdS2EgrN"); // Replace with your Daily.co room URL

    return {
      roomUrl,
    };
  },
};
</script>

<style>
#main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}
.video-call {
  width: 60%;
  height: 80%;
  border: 1px solid #ccc;
  margin-bottom: 20px;
}
</style>
