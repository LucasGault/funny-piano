<template>
    <div class="piano">
        <div @click="pianoPlay" class="toucheB"></div>
        <div class="toucheN"></div>
        <div class="toucheB"></div>
        <div class="toucheN"></div>
        <div class="toucheB"></div>
        <div class="toucheB"></div>
        <div class="toucheN"></div>
        <div class="toucheB"></div>
        <div class="toucheN"></div>
        <div class="toucheB"></div>
        <div class="toucheN"></div>
        <div class="toucheB"></div>
    </div>
</template>


<script lang="js">
    export default {
        name: 'Piano',
        methods: {
            pianoPlay() {
               console.log("touche")
            }
        }
    }
</script>


<style lang="postcss" scoped>
    .piano {
        @apply mx-auto bg-black flex justify-between relative p-3 mx-6;
        border-radius: 10px;
        height: 189px;
        width: 368px;
    }

    .toucheB {
        @apply bg-white;
        height: 166px;
        width: 47px;
    }

    .toucheN {
        @apply bg-black absolute;
        height: 120px;
        width: 20.79px;
        border-radius: 0px 0px 5px 5px;
        top: 6.5%;
    }

    .toucheB:first-child {
        border-radius: 5px 0px 0px 5px;
    }

    .toucheB:last-child {
        border-radius: 0px 5px 5px 0px;
    }

    .toucheB:hover,
    .toucheB:active {
        @apply bg-yellow-touche;
    }

    .toucheN:hover,
    .toucheN:active {
        @apply bg-purple-touche;
    }

    .piano div:nth-child(2) {
        left: 12.81%;
    }

    .piano div:nth-child(4) {
        left: 26.55%;
    }

    .piano div:nth-child(7) {
        left: 54.05%;
    }

    .piano div:nth-child(9) {
        left: 67.8%;
    }

    .piano div:nth-child(11) {
        left: 81.54%;
    }

    @screen md {
        .piano {
            @apply mx-auto;
            height: 276px;
            width: 531px;
        }

        .toucheB {
            height: 252px;
            width: 69px;
        }

        .toucheN {
            height: 184px;
            width: 30px;
            top: 4.35%;
        }
    }
</style>