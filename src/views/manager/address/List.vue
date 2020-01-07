<template>
<briup-fulllayout title="常用地址">
    <van-list>
    <van-cell
        v-for="item in address"
        :key="item.id"
        :title="item.province+' '+item.city+' '+item.area+' '+item.address"
    />
    </van-list>
    <br>
    <van-button block type="default" @click="toAddressEditHandler">
        添加
    </van-button>
</briup-fulllayout>
</template>

<script>
import {get} from '../../../http/axios'
import {mapState} from 'vuex'
export default {
    data(){
        return{
            address:[]
        }
    },
    computed:{
        ...mapState("user",["info"])
    },
    created(){
        this.loadAddress();
},
    methods:{
    loadAddress(){
            let id=this.info.id;
            let url="/address/findByCustomerId?id="+id;
            get(url).then((response)=>{
                this.address=response.data;
            })
    },
    toAddressEditHandler(){
        this.$router.push("/manager/address_edit");
    }
}
}
</script>
