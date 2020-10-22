<template>
    <div class="emoji">
        
    </div>
    
</template>


<script lang="js">
export default {
    methods: {
        
    } 
}
</script>

<style lang="postcss" scoped>

    .emoji{
        @apply bg-white mx-auto mt-12 mb-24;
        width: 200px;
        height: 200px;
    }

    @screen lg {
        .emoji {
            @apply bg-black mx-auto mt-8 mb-16;
        }
    }

</style>