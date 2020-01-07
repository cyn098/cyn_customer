<template>
    <briup-fulllayout title="新增地址">
     <!-- {{info}} -->
    <div>
        <van-cell-group>
           <van-field v-model="form.telephone" placeholder="手机号" />
        </van-cell-group>
        <van-cell-group>
           <van-field v-model="form.province" placeholder="省" />
        </van-cell-group>
        <van-cell-group>
           <van-field v-model="form.city" placeholder="市" />
        </van-cell-group>
        <van-cell-group>
           <van-field v-model="form.area" placeholder="区" />
        </van-cell-group>
        <van-cell-group>
           <van-field v-model="form.address" placeholder="详细地址" />
        </van-cell-group>

        <van-button block color="linear-gradient(to right, #4bb0ff, #6149f6)"  @click="submitHandler">保存 </van-button>
    </div>
    </briup-fulllayout>
</template>
<script>
import {post} from '../../../http/axios'
import {mapState} from 'vuex'
export default {
    data(){
        return{
            form:{}
        }
    },
    computed:{
        ...mapState('user',['info'])
    },
    methods:{
        submitHandler(){
            let url = "/address/saveOrUpdate";
            this.form.customerId = this.info.id;//在提交前，将当前登录者的id作为顾客id
            post(url,this.form).then((response)=>{
                this.$router.go(-1);//返回上一级页面
                this.$toast.success(response.message)//轻提示，提示成功

            })
        }
    }
    
}
</script>