<template>
    <div class="player-footer">
        <PlayerControls />
        <PlayerInfo :artist="artist"/>
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
        padding: 30px 10px;
    }
</style>
