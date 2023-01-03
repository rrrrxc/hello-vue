<template>
    <div>
    <div >受控数字：{{ number }}</div>
    <div v-if="!showName" v-loading="!showName"></div>  
    <div v-else>{{user.info.name }}</div>
    </div>
    
</template>

<script>
// import {EventBus, EventType} from './EventBus'
import {MittBus, MittType} from './MittEvent'
export default {
    name: "ParentControl",
    props: ['refresh','user'],
    data: function () {
        return {
            number: 0,
            showName:false
        }
    },
    watch: {
        refresh: function () {
            this.addOne()
        },
        user : {
            handler: function(newvalue) {
                if(newvalue?.info?.name)
                {
                    this.showName =true
                }
                
            },
            deep:true
        }
    },
    methods: {
        addOne() {
            this.number = this.number + 1;
        }
    },
    mounted() {
        // EventBus.$on(EventType.DATA_TYPE, (msg) => {
        //     console.log(msg)
        //     this.addOne()
        // })
        MittBus.on(MittType.DATA_TYPE, (msg) => {
            console.log(msg)
            this.addOne()
        })
     
    }

}
</script>