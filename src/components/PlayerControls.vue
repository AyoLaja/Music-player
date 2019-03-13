<template>
    <div class="player-controls">
        <div class="controls-container">
            <audio class="myAudio" :src="trackSrc">
                Your browser does not support the audio element.
            </audio>
            <span class="prev-track" @click="prevTrack()"></span>
            <span v-if="playing" class="pause-track" @click="pause()"></span>
            <span v-else class="play-track" @click="play()"></span>
            <span class="next-track" @click="nextTrack()"></span>
        </div>
        <div class="progress-container">
            <div class="progress-bar">
                <div class="progress-filled" :style="{flexBasis: progressPercentage}"></div>
            </div>
            <div class="timer">
                <p class="time">{{currentTime}} / {{durationTime}}</p>
            </div>
        </div>
    </div>
</template>

<script>
    import { eventBus } from '../main'   
    export default {
        data() {
            return {
                audio: undefined,
                progress: undefined,
                playing: false,
                progressPercentage: '0%',
                current: 0, //in seconds
                duration: 0
            }
        },
        mounted() {            
            this.audio = this.$el.querySelector('.myAudio')
            this.audio.addEventListener('loadeddata', this.load)
            this.audio.addEventListener('play', this.play)
            this.audio.addEventListener('pause', this.pause)
            this.audio.addEventListener('timeupdate', this.handleProgress);
        },
        props: {
            trackSrc: {
                type: String, 
                required: true
            }
        },
        methods: {
            load() {
                if (this.audio.readyState >= 2) {
                    this.duration = parseInt(this.audio.duration);
                }  
            },
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
            },
            handleProgress() {
                this.progressPercentage = (this.audio.currentTime / this.audio.duration) * 100 + '%';
                this.current = parseInt(this.audio.currentTime)
            },
            convertTime(val) {
                let hhmmss = new Date(val * 1000).toISOString().substr(11, 8);
                return hhmmss.indexOf("00:") === 0 ? hhmmss.substr(3) : hhmmss;
            }
        },
        watch: {
            current(val) {
                if (val === this.duration) {
                    this.nextTrack()
                }
            }
        },
        computed: {
            currentTime() {
                return this.convertTime(this.current)
            },
            durationTime() {
                return this.convertTime(this.duration)
            },
            scrubTime() {
                return this.convertTime(this.scrubed)
            }
        }
    }
</script>

<style scoped>
    .player-controls {
        width: 30%;
        text-align: center;
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

    span:last-of-type {
        margin-right: 0px;
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

    .progress-container {
        padding: 10px;
    }

    .progress-bar {
        flex: 10;
        position: relative;
        display: flex;
        flex-basis: 100%;
        height: 5px;
        transition: height 0.3s;
        background: #ccc;
        cursor: pointer;
        border-radius: 2px;
    }

    .progress-filled {
        width: 50%;
        background: #3db986;
        flex: 0;
        flex-basis: 50%;
        border-radius: 5px;
    }

    .timer {
        padding-top: 10px;
    }

    .time {
        font-size: 11px;
        width: 100%;
    }
</style>