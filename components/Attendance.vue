<template>
  <v-row justify="center">
    <v-col md="6" class="text-center">
      <v-card>
        <v-card-text>
          <video
            ref="video"
            autoplay
            :class="camera === 'user' ? 'flipX' : ''"
            width="100%"
          ></video>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            v-if="camera === 'environment'"
            icon
            fab
            @click.stop="reverseCamera('user')"
            ><v-icon color="green darken-3">mdi-camera-outline</v-icon></v-btn
          >
          <v-btn
            v-if="camera === 'user'"
            icon
            fab
            @click.stop="reverseCamera('environment')"
            ><v-icon color="green darken-3">mdi-fingerprint</v-icon></v-btn
          >
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      date: new Date().toISOString().substr(0, 10),
      modal: false,
      mediaStream: null,
      camera: 'user',
    }
  },
  computed: {
    rearCamera: {
      get() {
        return this.camera
      },
      set(value) {
        // Stop video stream
        this.$refs.video.srcObject &&
          this.$refs.video.srcObject.getTracks().map((track) => track.stop())
        // Assign facingmode
        this.camera = value
        // Start video stream
        this.init()
      },
    },
  },
  mounted() {
    this.init()
  },
  methods: {
    reverseCamera(value) {
      this.rearCamera = value
    },
    init() {
      if (
        navigator.getUserMedia ||
        navigator.webkitGetUserMedia ||
        navigator.mozGetUserMedia ||
        navigator.msGetUserMedia ||
        navigator.oGetUserMedia
      ) {
        navigator.mediaDevices
          .getUserMedia({
            video: { facingMode: this.camera },
          })
          .then((mediaStream) => {
            this.mediaStream = mediaStream
            this.$refs.video.srcObject = mediaStream
            this.$refs.video.play()
          })
      } else {
        alert('Cannot get media devices')
      }
    },
  },
}
</script>

<style scoped>
.flipX {
  transform: scaleX(-1);
}
</style>
