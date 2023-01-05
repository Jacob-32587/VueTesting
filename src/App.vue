<script>
import ChildComp from "./components/ChildComp.vue";

export default 
{
  components: {
    ChildComp
  }, // Comp
  data() 
  {
    return {
      greeting: 'Hello from parent',
      response: ''
    }
  } // Data
}
</script>

<template>
  <ChildComp :msg="greeting" @response="(m) => response = m"> _ </ChildComp>
  <p>{{ response }}</p>

  <ChildComp>
    Message in child: {{greeting}}
  </ChildComp>
</template>