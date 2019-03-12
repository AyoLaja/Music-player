<template>
    <div class="music-player">
        <h4>Music Player</h4>
        <br/>
        <PlayerImage coverImage="https://s3-us-west-1.amazonaws.com/fbx-fed-homework/Normcore_-_Neighbors/Normcore_-_01_-_The_Plane.jpg"/>
        <PlayerFooter :artist="artist"/>
    </div>
</template>

<script>
    import axios from 'axios'
    import { playlist } from '../resources/playlist'
    import PlayerImage from './PlayerImage.vue'
    import PlayerFooter from './PlayerFooter.vue'
    import PlayerControls from './PlayerControls.vue'
    import PlayerInfo from './PlayerInfo.vue'
    
    export default {
        data() {
            return {
                album: playlist.album_name,
                artist: playlist["artist"],
                myPlaylist: playlist.tracks
            }
        },
        created() {
            // this.getPlaylist()
            console.log(this.artist)
        },
        methods: {
            getPlaylist() {
                const apiUrl = 'https://s3-us-west-1.amazonaws.com/fbx-fed-homework/fed_home_assignment_api.json'

                axios.get(apiUrl, {
                    headers: {
                        "Access-Control-Allow-Origin": "*"
                    }
                })
                .then(response => console.log(response))
                .catch(error => console.log(error))
            }
        },
        components: {
            PlayerImage,
            PlayerFooter,
            PlayerImage,
            PlayerInfo
        }
    }
</script>

<style scoped>
    .music-player {
        height: 500px;
        width: 500px;
        margin: 0;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
</style>