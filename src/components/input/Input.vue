<script>
export default {
  name: "Input",
  data() {
    return {
      
    }
  }
};
</script>
<template>
  <input class="input" placeholder="" type="" />
</template>
<style scoped lang="scss">
.input {
  padding: 14px 20px;
  width: 100%;
  box-sizing: border-box;
  background-color: transparent;
  font-size: 16px;
  color: #fff;
  border: 1px solid #3d3d3d;
  border-radius: 5px;

  &:focus {
    outline: 1px solid #4b72c2;
  }
}
</style>
