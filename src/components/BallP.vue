<template>

<ball-c :ball="inner" @play-ball="getChild"></ball-c>
</template>

<script>
import BallC from './BallC.vue'

export default {
    name : 'BallP',
    components : {
        BallC
    },
    data :function () {
        return {
            inner :0
        }
    },
    methods : {
        getChild(ball) {
            console.log('子级踢给父级的是'+ball)
            this.inner=ball+1;
        }
    }
}
</script>