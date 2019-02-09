<template>
  <div id="index">
    <Button size="mini" color="green" angle="right">按钮 </Button>
  </div>
</template>

<script>
import Button from "@/components/Button.vue";

export default {
  name: "Index",
  components: {
    Button
  }
};
</script>

<style lang="less" scoped>
#index {
  padding: 10px;
}
</style>
