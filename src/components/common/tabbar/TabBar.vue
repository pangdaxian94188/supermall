<template>
  <div id="tab-bar">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: 'TabBar'
  }

</script>

<style>
  @import "/src/assets/css/base.css";

  #tab-bar {
    display: flex;
    background-color: #f6f6f6;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    border-top: 1px solid rgba(100, 100, 100, 0.1);
    box-shadow: 0 -1px 1px rgba(150, 150, 150, 0.1);
  }

</style>
