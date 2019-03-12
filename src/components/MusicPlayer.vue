<template>
    <div class="music-player">
        <h4>Music Player</h4>
        <br/>
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
                album: playlist.album_name,
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
</style>