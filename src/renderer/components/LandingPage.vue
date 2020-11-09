<template>
  <div>
    <h2>原神圣遗物属性推荐工具</h2>
    <h3 class="tips">众所周知有元素伤害，优先选择元素伤害</h3>
    <main>
      <el-col v-if="flag" :span="9">
        <h3>总攻击力</h3>
        <el-input
        placeholder="请输入内容"
        oninput="value=value.replace(/[^\d]/g,'')"
        v-model="agg1"
        clearable>
        </el-input>
        <h3>白字攻击力</h3>
        <el-input
        placeholder="请输入内容"
        oninput="value=value.replace(/[^\d]/g,'')"
        v-model="agg2"
        clearable>
        </el-input>
        <el-button @click="powerforceisgood">素质鉴定</el-button>
      </el-col>
      <el-col v-if="flag===false" :span="9">
        <h3>攻击力</h3>
        <el-input
        placeholder="请输入内容"
        oninput="value=value.replace(/[^\d]/g,'')"
        v-model="atk"
        clearable>
        </el-input>
        <h3>暴击</h3>
        <el-input
        placeholder="请输入内容"
        oninput="value=value.replace(/[^\d]/g,'')"
        v-model="ctr"
        clearable>
        </el-input>
        <h3>爆伤</h3>
        <el-input
        placeholder="请输入内容"
        v-model="ctd"
        oninput="value=value.replace(/[^\d]/g,'')"
        clearable>
        </el-input>
        <el-button @click="which">我该堆啥？</el-button>
      </el-col>
    </main>
    <footer class="ft">
      <h3>算法提供:b站up主
        <el-link href="https://space.bilibili.com/184421129" target="_blank">讲故事的勺子啊啊啊</el-link>
        </h3>
    </footer>
  </div>
</template>

<script>
 export default {
    data() {
      return {
        agg1: '',
        agg2: '',
        flag: true,
        atk: '',
        ctr: '',
        ctd: '',
      }
    },
    methods:{
      powerforceisgood:function(){
        //console.log(this.agg1/this.agg2);
        let msg={
          a:'还堆啥啊老实堆攻击去吧',
          b:'别往后看了'
        }
        
        if((this.agg1/this.agg2)>=2.1){
          msg.a='大佬请上座';
          msg.b='请您继续输入';
          this.flag=false;
        }
        this.$alert(msg.a, msg.b, {
          confirmButtonText: '确定',
        });
      },
      which:function(){
        const a = 3*(1+parseInt(this.ctr)*parseInt(this.ctd));
        const b = 2*(parseInt(this.atk)*parseInt(this.ctd));
        const c = 4*(parseInt(this.atk)*parseInt(this.ctr));
        let text;
        if(a>b&&a>c){
           text='我觉得大佬宁应该提升攻击';
        }else if(b>a&&b>c){
           text='我觉得大佬宁应该提升暴击';
        }else{
           text='我觉得大佬宁应该提升暴伤';
        }
        this.$alert(text, '建议', {
          confirmButtonText: '确定',
        });
      }
    }
  }
</script>

<style>
.tips{
  color: chocolate;
}
.ft{
  position: absolute;
  right:50px;
  bottom: 50px;
}
</style>
