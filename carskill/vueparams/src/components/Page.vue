<!--
 * @Author: your name
 * @Date: 2019-11-29 19:11:58
 * @LastEditTime: 2019-12-01 19:36:20
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vueparams\src\components\Page.vue
 -->
<template>
    <div class="page">
        <!-- 渲染 -->
        <div v-for="(item,index) in Arr" :key="index" >
            <div class="letter" :id="index">{{item.newletter}}</div>
            <div >{{item.children.Name}}</div>
       <div v-for="(ite,ind) in item.children" :key="ind" class="box">  
           <div class="rend">               
               <img :src="ite.CoverPhoto" class="img"/>
               <span class="name" @click="animation(ite.Name)">{{ite.Name}}</span>
           </div>
       </div>
        </div> 

    <!-- 楼层 -->
    <div class="floor">
        <li v-for="(item,index) in Arr" :key="index" >
            <a :href="'#'+index">{{item.newletter}}</a>
            
        </li>
    </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    props:{
       
    },
    components:{

    },
    data(){
        return {
         newData:[],
         Arr:[],
       
    
        }
    },
    computed:{

    },
    methods:{
        animation(item){
            console.log(item)
        }
    },
    created(){

    },
    mounted(){
        axios.get('https://baojia.chelun.com/v2-car-getMasterBrandList.html').then(res=>{
            // console.log(res.data.data)
            //axios请求过来的数据 
            if(res.data.code==1){
            //循环此数据 将字母(A-Z)循环截取出来
                this.newData=res.data.data
             this.newData.map((item,index)=>{    //循环
                let newletter=item.Spelling[0]  //拿到A-Z
                //  console.log(newletter)
                let newArr=this.newData.filter(item=>item.Spelling[0]==newletter) //过滤出与A-Z相同的数据
                //  console.log(newArr)
                 if(this.Arr.findIndex(item=>item.newletter==newletter)===-1){ // 因为有很多条相同的数据 故声明一个空数组 用findIndex查找 空数组若没有相同数剧则push 
                     this.Arr.push({newletter,children:newArr})
                 }
             })
                     console.log(this.Arr)
                
            }

                    //  this.newletter=Array.from(new Set(this.newletter))    //es6去重方法
                  
        })
    }
}
</script>
<style scoped lang="style.css">

    .page{
        width: 100%;
        height: 100%;
    }

    .letter{
        width: 100%;
        height: 40px;
        background: #eee;
        line-height: 40px;
    }
    .box{
        width: 90%;
    }
    .rend{
        width: 100%;
        height: 50px;
        line-height: 50px;
        border-bottom: 1px solid #ccc;
        display: flex;
        margin-left: 10px;
        margin-right: 10px;


    }
    .rend :last-child{
        border-bottom: none;
    }
    .img{
        width: 15%;
        height: 100%;
    }
    .name{
        display: block;
        width: 150px;
       height: 50px;
        line-height: 50px;
        /* background: blue; */
        padding-left: 20px;
    }

    .floor{
        position: fixed;
        right: 10px;
        top: 100px;
        font-size: 8px;
    }
    .floor li{
        list-style: none;
        height: 15px;
        line-height: 15px;

    }
    a{
        text-decoration: none;
        color:#333;

    }
</style>