<template>
    <div>
        <el-card class="box-card">
            <div slot="header">
                <el-button @click="fresh">控制子组件</el-button>
            </div>
            <parent-control ref="child" :refresh="refresh" :user="user"/>
        </el-card>
    </div>
</template>
<script>
// import {EventBus, EventType} from './util/EventBus'
import {MittBus, MittType} from './util/MittEvent'
import ParentControl from './util/ParentControl.vue'
export default {
    name: 'MainComp',
    components: {
        ParentControl
    },
    data: function() {
        return {
            refresh: false,
            user: {
             
            }
        }
    },
    mounted() {
        setTimeout(()=> {
           this.$set(this.user,'info',{name:'大象'})
            },3000)
    },

    

    
    methods: {
        fresh() {
            //方法四
            MittBus.emit(MittType.DATA_TYPE, '童叟无欺Mitt')
            // 方法三
            // EventBus.$emit(EventType.DATA_TYPE, '童叟无欺')
              // 方法二
            // this.$refs.child.addOne()
            // console.log(this.$refs)
            //方法一
            // this.refresh = !this.refresh;
        }
    },

}
</script>