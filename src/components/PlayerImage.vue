<template>
    <div class="player-image">
        <img :src="coverImage" alt="Cover image"/>
    </div>
</template>

<script>
    export default {
        props: {
            coverImage: {
                type: String,
                required: false
            }
        }
    }
</script>

<style scoped>
    .player-image {
        height: inherit;
        width: inherit;
    }

    img {
        width: inherit;
    }
</style>