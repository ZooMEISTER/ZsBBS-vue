<template>
    <div style="height: 10px;"/>
    <div>
        <div style="display: flex; flex-direction: row; width: 70%; margin: auto;">
            <!-- 面包屑 -->
            <el-breadcrumb class="breadscrumb_1">
                <el-breadcrumb-item :to="{ path: '/zsbbs/forum' }">
                    <h2>论坛</h2>
                </el-breadcrumb-item>
            </el-breadcrumb>

            <!-- <div style="width: 50%;"/> -->

            <div style="display: flex; flex-direction: row; margin: auto;">
                <el-text type="primary">排序依据:&nbsp;&nbsp;</el-text>
                <el-select v-model="name_sortby" placeholder="Select" size="large" @change="changeSelectSortby($event)">
                    <el-option
                        v-for="item in sortby"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value"
                    />
                </el-select>
                <el-text type="primary">&nbsp;&nbsp;BY:&nbsp;&nbsp;</el-text>
                <el-select v-model="name_sequence" placeholder="Select" size="large" @change="changeSelectSequence($event)">
                    <el-option
                        v-for="item in sequence"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value"
                    />
                </el-select>
            </div>

        </div>
        <!-- 显示帖子的组件 0 为广场上的帖子 -->
        <Comp_ShowAllPost 
            :p_postType=0
            :p_postDesc="value_sequence"
            :p_sortby="value_sortby"
            ref="ref_Comp_ShowAllPost"
        ></Comp_ShowAllPost>
        
    </div>
    
    <!-- 添加新的post的按钮 -->
    <el-button class="btn_addPost" type="primary" size="large" @click="addNewPost">发帖</el-button>

    <!-- 回到顶部按钮 -->
    <el-backtop :right="200" :bottom="200" />
</template>

<script>
import axios from 'axios'
import Comp_ShowAllPost from "./showpost.vue"

export default {
    components:{
        Comp_ShowAllPost
    },
    data(){
        return{
            sortby:[
                {
                    value: 'rt',
                    label: '回复时间',
                },
                {
                    value: 'pt',
                    label: '发布时间',
                },
            ],
            sequence:[
                {
                    value: true,
                    label: '最新',
                },
                {
                    value: false,
                    label: '最旧',
                },
            ],
            name_sortby: "回复时间",
            name_sequence: "最新",
            value_sortby: "rt",
            value_sequence: true,
        }
    },
    created(){
        
    },
    methods:{
        //添加新的post
        addNewPost(){
            console.log("add new post")
            //先判断用户有没有登录
            if(this.$store.state.s_userid == -1){
                this.$message.error('Please Login first')
                return
            }
            this.$router.push('/zsbbs/forum/addnewpost')
        },
        changeSelectSortby(e){
            //console.log("e --- " + e)
            this.value_sortby = e
            //console.log("e.value --- " + e.value)
            this.$refs.ref_Comp_ShowAllPost.getAllPosts(this.value_sortby, this.value_sequence)

        },
        changeSelectSequence(e){
            this.value_sequence = e
            //console.log("e.value --- " + e.value)
            this.$refs.ref_Comp_ShowAllPost.getAllPosts(this.value_sortby, this.value_sequence)
        }
        
    }
}
</script>


<style>
.btn_addPost {
  position: fixed;
  top: 120px;
  right: 100px;
  right: 200px;
  width: 75px;
  height: 75px;
}
</style>