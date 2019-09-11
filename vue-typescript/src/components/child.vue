<template>
    <div @click="clickEvent">我是子组件{{name}}
        <p>{{propA}}{{propB}}</p>
        <div @click="clickEvent1">子组件与父组件通信，返回参数</div>
    </div>
</template>
<script lang="ts">
import {Component,Prop,Emit,Watch,Vue} from 'vue-property-decorator'

//Props可以单独使用@Prop或这保持2.x的风格，在@Component注解里统一声明
@Component({
    props:{
     name:String   
    }
})
export default class Child extends Vue{
   private obj:Object={
       key1:'1',
       key2:'2'
   }
   @Prop() private name!:string  //propd第一种形式
   @Prop()   //第二种，实际同上
   propA!:string

   @Prop()
   propB:number=22222222  //第三种方式，= 赋初值,不建议，会在页面报错，prop应该是静态值不可改变，可通过第四种方式赋初值

    @Prop([String, Boolean])
    propC!: string | boolean

   @Emit('hhhh')
   public clickEvent():void{
       
   }
   @Emit()
   /**
    * clickEvent1
    */
   public clickEvent1(obj:Object) {
       debugger
   }

}
</script>