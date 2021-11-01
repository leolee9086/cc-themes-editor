<template>
    <div>
    <el-row>
    <el-select 
    @focus="getAssets()"
    v-model="filepath"
    size=mini>
        <el-option
        v-for="(item,i) in filesArry"
        :key="i"
        :label="item.name.replace(/<mark>/g,'').replace(/<\/mark>/g,'')"
        :value="item.path"
        >
        </el-option>
    </el-select>
    </el-row>
    
    <div>
</template>
<script>
module.exports = {
    props:["k",'value','apitoken'],
    model:{
        props:"value",
        event:"change"
    },
    mounted() {
        this.$nextTick(this.getAssets())
        
    },
    data() {
        return {
            filesArry:[],
            filepath:"",
            hosturl:vm.hosturl
        }
    },
    watch:{
        k:{
            handler(val,oldval){
                this.getAssets(val)
            }
        },
        filepath:{
            
            handler(val,oldval){
                this.$emit("change",'http://'+vm.hosturl+'/'+val)
            }
        }
    },
    methods: {

        getAssets:  function(){
            let that = this
            let jsondatas = {"k":that.k}
             axios({
                        method:'POST',
                        url:'http://'+vm.hosturl + '/api/search/searchAsset',
                        headers:{'Authorization': 'Token '+ that.apitoken },
                        data:(jsondatas)
                        }).then(result =>{
                        that.filesArry =  result.data["data"]
                        })
            }
        
    },
    
}

</script>
 
<style>

</style>