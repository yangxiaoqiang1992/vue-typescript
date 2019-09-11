<template>
    <div>hello,{{name}},{{age}}<p>{{msg}}</p>{{n}}{{fullName}}{{obj.obj1}}
      <input v-model='obj.obj1' ref="input"/>{{obj.obj2}}
      <child ref="child" :name="n" :propA ='11111' @clickEvent1="clickEvent1"/>
    </div>
</template>

<script lang="ts">
import {Component,Prop,Emit,Watch,Vue} from 'vue-property-decorator'
import Child from './child.vue'
interface Person {
    name:string,
    age:number,
    sex?:string
}
@Component({
    components:{
      Child
    }
})
export default class Demo extends Vue{

   //data里的属性直接声明即可，或者再construtor方法里赋初值 
   public n:string = 'ddd'
   private obj:Object ={obj1:'2233',obj2:''};
   //prop父组件prop值，加！非空断言不是必须的，但能防止编译器报错,readonly表示只读
   @Prop() private readonly msg!: string; 
   @Prop() private  name!: string;
   @Prop({default:'demo',type:[String,Number]}) private age!:string | number

   //watch监听
   @Watch('n')
   private  ageChange(val:string,oldval:string){
       console.log('watch',val)
   }
   //watch 深度监听
   @Watch('obj',{deep:true})
   private getObject(val:object){
       console.log('obj',val)
   }
   //computed 使用get set的形式
   get fullName(){
       return this.name +'dddd'
   }
   //set name,不可以写返回值类型，void也不行
   set fullName(val){
       this.name = val  
   }
   //类型自定义
   //接口定义数据结构
   getPerson(person:Person):string{
       console.log('person',person)
     return `${person.name}/${person.age}/${person.sex}`
   }
   //父组件监听子组件传值
   clickEvent1(val:Object){
       debugger
       console.log('父组件监听到回传参数',val)
   }
   public mounted():void{
       this.n ='yyyy'
       this.getPerson({
           name:'zhangshan',
           age:12
       })
      this.getPerson({
           name:'lisi',
           age:88
       })
      this.getPerson({
           name:'王五',
           age:88,
           sex:'男'
       })
       //获取元素或组件实例，使用$refs  
       console.log(this.$refs.child)
       console.log(this.$refs.input)
   }
   constructor(){
       super()
      // this.n = 'yyyy'
   }
}
</script>