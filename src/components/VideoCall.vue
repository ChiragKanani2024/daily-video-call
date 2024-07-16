<template>
  <div class="video-call-container">
    <div ref="callFrameRef" class="call-frame"></div>
  </div>
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from "vue";
import DailyIframe from "@daily-co/daily-js";

export default {
  name: "VideoCall",
  props: {
    roomUrl: {
      type: String,
      required: true,
    },
  },
  setup(props) {
    const callFrameRef = ref(null);
    let callFrame = null;

    const startCall = () => {
      callFrame = DailyIframe.createFrame(callFrameRef.value, {
        iframeStyle: {
          height: "100%",
          width: "100%",
          aspectRatio: 16 / 9,
          border: "1px solid var(--grey)",
          borderRadius: "4px",
        },
        showLeaveButton: true,
      });

      callFrame.join({ url: props.roomUrl }).catch((error) => {
        console.error("Failed to join the call:", error);
      });
    };

    const leaveCall = () => {
      if (callFrame) {
        callFrame.leave().catch((error) => {
          console.error("Failed to leave the call:", error);
        });
      }
    };

    onMounted(() => {
      startCall();
    });

    onBeforeUnmount(() => {
      leaveCall();
    });

    return {
      callFrameRef,
    };
  },
};
</script>

<style>
.call-frame {
  width: 100%;
  height: 100%;
}
.video-call-container {
  width: 100%;
  height: 100%;
}
</style>
