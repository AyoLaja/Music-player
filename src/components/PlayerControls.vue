<template>
    <div class="player-controls">
        <audio class="myAudio" :src="trackSrc">
            <!-- <source type="audio/mp3"> -->
        </audio>
        <span @click="prevTrack()">
            <img src="../assets/Fundbox/Assets/back_idle.png" alt="Previous Track"/>
        </span>
        <span @click="play()">
            <img src="../assets/Fundbox/Assets/play_idle.png" alt="Play Track"/>
        </span>
        <span @click="nextTrack()">
            <img src="../assets/Fundbox/Assets/forward_idle.png" alt="Next Track"/>
        </span>
    </div>
</template>

<script>
    import { eventBus } from '../main'      

    const audio = document.querySelector('.myAudio')

    export default {
        // data() {
        //     return {
        //         track: trackSrc
        //     }
        // },
        methods: {
            play() {
                console.log(audio)
                // audio.play ? audio.pause() : audio.play()
                if (audio.play) {
                    this.pause()
                    console.log('audio was playing, now pasued')
                }
                else {
                    audio.play()
                }
                // audio.addEventListener('play', audio.play)
                // audio.play()
            },
            pause() {
                audio.pause()
            },
            nextTrack() {
                eventBus.$emit('nextTrack')
                audio.play()
            },
            prevTrack() {
                eventBus.$emit('prevTrack')
                audio.play()
            }
        },
        props: {
            trackSrc: {
                type: String, 
                required: true
            }
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