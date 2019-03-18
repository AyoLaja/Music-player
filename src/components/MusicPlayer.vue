<template>
    <div class="music-player">
        <PlayerImage :coverImage="currentTrack.cover_image"/>
        <PlayerFooter :artist="artist" :trackName="currentTrack.name" :trackSrc="currentTrack.url"/>
    </div>
</template>

<script>
    import axios from 'axios'
    import { playlist } from '../resources/playlist'
    import PlayerImage from './PlayerImage.vue'
    import PlayerFooter from './PlayerFooter.vue'
    import PlayerControls from './PlayerControls.vue'
    import PlayerInfo from './PlayerInfo.vue'
    import { eventBus } from '../main'
    
    export default {
        data() {
            return {
                artist: playlist.artist,
                currentTrack: playlist.tracks[0],
                trackNumber: 0
            }
        },
        components: {
            PlayerImage,
            PlayerFooter,
            PlayerImage,
            PlayerInfo
        },
        created() {
            // this.getPlaylist()
            eventBus.$on('prevTrack', () => {
                if (this.trackNumber <= 0) {
                    this.trackNumber = playlist.tracks.length - 1
                    this.currentTrack = playlist.tracks[this.trackNumber]
                }
                else {
                    this.trackNumber--
                    this.currentTrack = playlist.tracks[this.trackNumber]
                }
            })

            eventBus.$on('nextTrack', () => {
                if (this.trackNumber >= playlist.tracks.length - 1) {
                    this.trackNumber = 0
                    this.currentTrack = playlist.tracks[this.trackNumber]
                }
                else {
                    this.trackNumber++
                    this.currentTrack = playlist.tracks[this.trackNumber]
                }
            })
        },
        methods: {
            //Ran into CORS error while trying to make the request to the resource 
            getPlaylist() {
                const apiUrl = 'https://s3-us-west-1.amazonaws.com/fbx-fed-homework/fed_home_assignment_api.json'

                axios.get(apiUrl, {
                    headers: {
                        "Access-Control-Allow-Origin": "http://localhost:8081",
                        crossorigin: true
                    }
                })
                .then(response => console.log(response))
                .catch(error => console.log(error))
            }
        }
    }
</script>

<style scoped>
    .music-player {
        width: 500px;
        margin: 0;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    @media only screen and (max-width: 768px) {
        .music-player {
            width: 100%;
        }
    }
</style>