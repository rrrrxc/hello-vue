<template>
   <div>
    <el-input v-model="message"></el-input>
    <el-input v-model="name"></el-input>

    <div>反转之后的值：{{ reverseMsg }}</div>
   <div>需要发送给父级的数据<el-input v-model="localInfo"></el-input></div>
    <el-button @click="monitor">查看值</el-button>
   </div> 
</template>

<script>
export default {
    name: 'ChildComp',

    props : {
        info:String,
    },
    data: function() {
        return {
          message :'',
          name:'',
          localInfo:'',
          localCmRealValue:''
        }
    },

    computed : {
        reverseMsg:function () {
            return this.message.split('').reverse().join('')
        },
        //曲线救国：通过事件模式+computed的get/set，直接读取和修改父级信息
        localCm : {
            get: function () {
                return this.info
            },
            set:function (v) {
                this.$emit('updata-info',v)
            }
        }
    },

    watch : {
        name:function (newValue,oldValue) {
            console.log(newValue,oldValue)
        },
        message: {
            handler : function (newValue,oldValue) 
            {
                console.log('message',newValue,oldValue)
            },
            immediate:true
        },
        info:{
            handler : function (newValue,oldValue) 
            {
                console.log('message',newValue,oldValue)
                this.localInfo=newValue
            },
            immediate:true
        }
    },
    // // 生命周期函数
    // beforeCreate() {
    //     console.log('beforeCreate')
    // },
    // created() {
    //     console.log('created')
    // },
    // beforeMount() {
    //     console.log('beforeMount')
    // },
    // mounted() {
    //     window.addEventListener('click', this.handleEvent)
    //     // TODO: 初始化组件的数据
    //     // 异步逻辑
    //     // const res = await xxxx();
    //     console.log('mounted')
    // },
    // beforeDestroy() {
    //     console.log('beforeDestroy')
    // },
    // destroyed() {
    //     // 取消事件的订阅
    //     console.log('destroyed')
    //     window.removeEventListener('click', this.handleEvent)
    // },
    methods: {
        handleEvent() {
            console.log('吱吱吱')
        },
        monitor () {
            this.$emit('send-data', this.localInfo)
        }
    }
}
</script>

<style lang="scss" scoped>
</style>