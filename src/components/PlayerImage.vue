<template>
    <div class="player-image">
        <transition name="fade" mode="out-in">
            <img :src="coverImage" alt="Cover image"/>
        </transition>
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

<
<style scoped>
    .player-image {
        height: inherit;
        width: inherit;
    }

    img {
        width: inherit;
    }

    .fade-enter-active, .fade-leave-active {
        transition: opacity 0.5s;
    }

    .fade-enter, .fade-leave-to {
        opacity: 0;
    }
</style>