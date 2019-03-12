<template>
    <div class="player-controls">
        <audio class="myAudio" :src="trackSrc" controls>
            <!-- <source type="audio/mp3"> -->
        </audio>
        <span @click="prevTrack()">
            <img src="../assets/Fundbox/Assets/back_idle.png" alt="Previous Track"/>
        </span>
        <span v-if="playing" @click="pause()">
           
            <img src="../assets/Fundbox/Assets/pause_idle.png" alt="Pause Track"/>
        </span>
        <span v-else @click="play()">
             <img src="../assets/Fundbox/Assets/play_idle.png" alt="Play Track"/>
        </span>
        <span @click="nextTrack()">
            <img src="../assets/Fundbox/Assets/forward_idle.png" alt="Next Track"/>
        </span>
    </div>
</template>

<script>
    import { eventBus } from '../main'      

    // const audio = document.querySelector('.myAudio')
    // audio.addEventListener('play', )

    export default {
        data() {
            return {
                audio: undefined,
                playing: false
            }
        },
        methods: {
            play() {
                this.audio.play()
                this.playing = true
            },
            pause() {
                this.audio.pause()
                this.playing = false
            },
            nextTrack() {
                eventBus.$emit('nextTrack')
                this.playing = false
                setTimeout(() => {
                    this.play()
                }, 500);
            },
            prevTrack() {
                eventBus.$emit('prevTrack')
                this.playing = false
                setTimeout(() => {
                    this.play()
                }, 500);
            }
        },
        props: {
            trackSrc: {
                type: String, 
                required: true
            }
        },
        mounted() {
            this.audio = this.$el.querySelector('.myAudio')
            this.audio.addEventListener('play', this.play)
            this.audio.addEventListener('pause', this.pause)
        }
    }
</script>

<style scoped>
    .player-controls {
        width: 30%;
    }

    span {
        padding-right: 10px;
        cursor: pointer;
    }
</style>