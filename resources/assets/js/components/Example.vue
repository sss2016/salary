<template>
    <!--<el-row type="flex" justify="center" style="margin-top: 15%">-->
        <!--<el-col :span="6" >-->
<!--<el-card class="box-card">-->
    <!--<el-row type="flex" justify="center">-->
    <!--<h1>登陆</h1>-->
    <!--</el-row>-->
    <!--<el-row type="flex" justify="center">-->
        <!--<el-col >-->
        <!--<el-form label-width="80px">-->
            <!--<el-form-item label="用户名:">-->
                <!--<el-input placeholder="请输入账号"></el-input>-->
            <!--</el-form-item>-->
            <!--<el-form-item label="密码:" >-->
                <!--<el-input placeholder="请输入密码"></el-input>-->
            <!--</el-form-item>-->
            <!--<el-form-item label="类型:" >-->
                <!--<el-radio class="radio" v-model="radio" label="1">管理员</el-radio>-->
                <!--<el-radio class="radio" v-model="radio" label="2">用户</el-radio>-->
            <!--</el-form-item>-->
            <!--<el-form-item >-->
                <!--<el-button type="success" style="width: 100%" @click="getValue" >登陆</el-button>-->
            <!--</el-form-item>-->
        <!--</el-form>-->
        <!--</el-col>-->
    <!--</el-row>-->

<!--</el-card>-->
        <!--</el-col>-->
    <!--</el-row>-->
    <el-row class="demo-autocomplete">
        <el-col :span="12">
            <div class="sub-title">激活即列出输入建议</div>
            <el-autocomplete class="inline-input" v-model="state1" :fetch-suggestions="querySearch" placeholder="请输入内容" @select="handleSelect"></el-autocomplete>
        </el-col>
        <el-col :span="12">
            <div class="sub-title">输入后匹配输入建议</div>
            <el-autocomplete class="inline-input" v-model="state2" :fetch-suggestions="querySearch" placeholder="请输入内容" :trigger-on-focus="false" @select="handleSelect"></el-autocomplete>
        </el-col>
    </el-row>
</template>

<style>
    .mg{
        margin-right: 80px;
    }

</style>

<script>
    export default{
        data:function(){
             return{   radio:1,
                restaurants: [],
                state1: '',
                state2: ''
             }
        },
        methods:{
                getValue:function (h,cb) {
                    console.log("h："+h+"cb"+cb)
                },
            querySearch(queryString, cba) {
                var restaurants = this.restaurants;
                var results = queryString ? restaurants.filter(this.createFilter(queryString)) : restaurants;
                // 调用 callback 返回建议列表的数据
                cba(results);
            },
            createFilter(queryString) {
                return (restaurant) => {
                    return (restaurant.value.indexOf(queryString.toLowerCase()) === 0);
                };
            },
            loadAll() {
                return [
                    { "value": "三全鲜食（北新泾店）", "address": "长宁区新渔路144号" },
                    { "value": "Hot honey 首尔炸鸡（仙霞路）", "address": "上海市长宁区淞虹路661号" },
                    { "value": "新旺角茶餐厅", "address": "上海市普陀区真北路988号创邑金沙谷6号楼113" },
                    { "value": "泷千家(天山西路店)", "address": "天山西路438号" },
                    { "value": "胖仙女纸杯蛋糕（上海凌空店）", "address": "上海市长宁区金钟路968号1幢18号楼一层商铺18-101" },
                    { "value": "贡茶", "address": "上海市长宁区金钟路633号" },
                    { "value": "豪大大香鸡排超级奶爸", "address": "上海市嘉定区曹安公路曹安路1685号" },
                    { "value": "茶芝兰（奶茶，手抓饼）", "address": "上海市普陀区同普路1435号" },
                    { "value": "十二泷町", "address": "上海市北翟路1444弄81号B幢-107" }
                ];
            },
            handleSelect(item) {
                console.log(item);
            }
        },
        mounted() {
            this.restaurants = this.loadAll();
        }
    }
</script>