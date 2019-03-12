<template>
    <div class="player-controls">
        <span>
            <img src="../assets/Fundbox/Assets/back_idle.png" alt="back idle"/>
        </span>
        <span>
            <img src="../assets/Fundbox/Assets/play_idle.png" alt="back idle"/>
        </span>
        <span>
            <img src="../assets/Fundbox/Assets/forward_idle.png" alt="back idle"/>
        </span>
    </div>
</template>

<script>
    export default {
        methods: {
            play() {

            },
            nextTrack() {

            },
            prevTrack() {

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