<template>
    <div>
    <cc-assets-selector
    v-model="rawurl"
    :k="type"
    :apitoken="apitoken"
    >

    </cc-assets-selector> 
    <el-select 
    v-model="type"
    size="mini">
        <el-option
         v-for="item in filetypes"
         :key='item'
         :label='item'
         :value='item'
        ></el-option>
    </el-select>
    <el-row>
    <el-image 

    :src="rawurl"
    style="width: 150px; height: 150px"
    v-if="rawurl!=''"
    :fit="'scale-down'"
    :preview-src-list="[rawurl]"
    ></el-image>
    </el-row>
    </div>
</template>
<script>
module.exports = {
   components:{
           "cc-assets-selector":"url:components/cc-assets-selector.vue",
       },
    props:["filetypes",'value','apitoken'],
    model:{
        props:"value",
        event:"change"
    },
    data(){
        return{
            rawurl:"",
            type:".png",
            hosturl:vm.hosturl
        }
    },
    watch:{
        rawurl:{
         handler(val,oldval){
             this.$emit("change",'url('+val+')')
         },
        }

    }
    }
</script>
