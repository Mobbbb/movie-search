<template>
    <div id="app">
        <Index />
    </div>
</template>

<script>
import Index from './Views/Index.vue'

export default {
    name: 'App',
    components: {
        Index
    }
}
</script>

<style>
    html,body{
        height: 100%;
    }
    #app{
        height: 100%;
    }
</style>
