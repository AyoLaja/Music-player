<template>
    <div class="player-footer">
        <PlayerControls :trackSrc="trackSrc" />
        <PlayerInfo :artist="artist" :trackName="trackName"/>
    </div>
</template>

<script>
    import PlayerControls from './PlayerControls'
    import PlayerInfo from './PlayerInfo'
    
    export default {
        components: {
            PlayerControls, 
            PlayerInfo
        },
        props: {
            artist: {
                type: String,
                requried: true
            },
            trackName: {
                type: String, 
                required: true
            },
            trackSrc: {
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>
    .player-footer {
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: #fff;
        padding: 30px 20px;
        margin-top: -4px;
    }
</style>
