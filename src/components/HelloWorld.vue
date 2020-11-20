<template>
  <h1>{{ msg }}</h1>
  <button @click="increment">count is: {{ count }}</button>
  <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p>
  <p ref="newContent">这是新内容{{initValue}} 新数字 {{ newCount}}  乘2 {{ computeCount }}</p>
</template>

<script>
import { computed, onMounted, reactive, toRefs, watch } from "vue"
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  setup(props,context){
    let state = reactive({
      name:"idea",
      content:"今天要做的事",
      newCount:0
    })
    let initValue = props.msg;
    
    let increment = ()=>{
      state.newCount++;
      console.log("上下文",context.$refs.newContent);
    }

    let computeCount = computed(()=>{
      return state.newCount*2
    })

    onMounted(()=>{
      state.newCount = 3;
    })

    // 传一个对象，默认深度监听
    watch(state,()=>{
      console.log("count =" + state.newCount)
    })

    // 监听单个值
    watch(() => state.newCount, (oldVlaue, newValue) => {
      console.log(oldVlaue, newValue, '改变')
    })

    return {
      ...toRefs(state),
      initValue,
      increment,
      computeCount
    }
  },
  data() {
    return {
      count: 0
    }
  }
}
</script>
