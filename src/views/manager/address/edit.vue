<template>
    <briup-fulllayout title="新增地址">
    <div>
        {{form}}
        <van-cell-group>
            <van-field v-model="form.telephone" placeholder="输入手机号"/>
        </van-cell-group>
        <van-cell-group>
            <van-field v-model="form.province" placeholder="省"/>
        </van-cell-group>
        <van-cell-group>
            <van-field v-model="form.city" placeholder="市"/>
        </van-cell-group>
        <van-cell-group>
            <van-field v-model="form.area" placeholder="区"/>
        </van-cell-group>
        <van-cell-group>
            <van-field v-model="form.address" placeholder="输入详细地址"/>
        </van-cell-group>
        <van-button block type="primary" @click="submitHandler">保存</van-button> 
    </div>
    </briup-fulllayout>
</template>
<script>
import {mapState} from 'vuex'
import {post} from '../../../http/axios'
export default {
    computed:{
        //将状态机中的user对象中的info对象获取到
        ...mapState("user",["info"])
    },
    data(){
        return{
            form:{}
        }
    },
    methods: {
        submitHandler(){
            let url ="/address/saveOrUpdate";
            //给当前顾客添加地址
            this.form.customerId=this.info.id;
            post(url,this.form).then((response)=>{
                //返回上级页面
                this.$router.go(-1);
                this.$toast.success(response.message);
            });
        }
    }

}
</script>
<style scoped>

</style>