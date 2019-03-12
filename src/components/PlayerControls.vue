<template>
    <div class="player-controls">
        <audio class="myAudio" :src="trackSrc">
            Your browser does not support the audio element.
        </audio>
        <span class="prev-track" @click="prevTrack()"></span>
        <span v-if="playing" class="pause-track" @click="pause()"></span>
        <span v-else class="play-track" @click="play()"></span>
        <span class="next-track" @click="nextTrack()"></span>
    </div>
</template>

<script>
    import { eventBus } from '../main'      
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
        text-align: left;
    }

    span {
        margin-right: 10px;
        cursor: pointer;
        display: inline-block;
        height: 20px;
        width: 26px;
        background-repeat: no-repeat;
        background-size: contain;
    }

    .play-track, .pause-track {
        width: 16px;
    }

    .play-track {
        background: url('../assets/Fundbox/Assets/play_idle.png')
    }

    .play-track:hover {
        background: url('../assets/Fundbox/Assets/play_hover.png')
    }

    .pause-track {
        background: url('../assets/Fundbox/Assets/pause_idle.png')
    }

    .pause-track:hover {
        background: url('../assets/Fundbox/Assets/pause_hover.png')
    }

    .prev-track {
        background: url('../assets/Fundbox/Assets/back_idle.png')
    }

    .prev-track:hover {
        background: url('../assets/Fundbox/Assets/back_hover.png')
    }

    .next-track {
        background: url('../assets/Fundbox/Assets/forward_idle.png')
    }

    .next-track:hover {
        background: url('../assets/Fundbox/Assets/forward_hover.png')
    }

    .play-track, .pause-track, .next-track, .prev-track {
        transition: all 0.3s ease;
    }
</style>