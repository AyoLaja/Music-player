<template>
    <div class="player-info">
        <p>{{artist}}</p>
        <hr/>
        <p>Crazy in love</p>
    </div>
</template>

<script>
export default {
    props: {
        artist: {
            type: String,
            required: false
        },
        track: {
            type: String,
            required: false
        }
    }
}
</script>

<style scoped>
    .player-info {
        width: 70%;
        text-align: left;
    }

    hr {
        border: 1px solid #ddd;
        margin: 10px 0px;
    }

</style>