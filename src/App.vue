<script setup>
  import Tooltip from "@/components/Tooltip.vue";
</script>

<template>
  <header>
    <div class="wrapper">
      <Tooltip contents="Custom tooltip!" position="custom" :customPosition="['50', '50']" >
        <div class="red"></div>
      </Tooltip>
      <Tooltip contents="Top tooltip!" position="top">
       <div class="blue"></div>
      </Tooltip>
      <Tooltip contents="Left tooltip!" position="left">
        <div class="green"></div>
      </Tooltip>
      <Tooltip contents="Calculated, stylized tooltip!" color="dodgerblue"
               background="#fff" border="1px solid dodgerblue" borderRadius="20px">
        <div class="orange"></div>
      </Tooltip>
      <Tooltip contents="Right-down tooltip!" position="rightDown">
        <div class="orange"></div>
      </Tooltip>
      <Tooltip contents="Right-top tooltip!" position="rightTop">
        <div class="red"></div>
      </Tooltip>
      <Tooltip contents="Left-down tooltip!" position="leftDown">
        <div class="blue"></div>
      </Tooltip>
      <Tooltip contents="Left-top tooltip!" position="leftTop">
        <div class="green"></div>
      </Tooltip>
      <Tooltip contents="Down-right tooltip!" position="downRight">
        <div class="green"></div>
      </Tooltip>
      <Tooltip contents="Down-left tooltip!" position="downLeft">
        <div class="orange"></div>
      </Tooltip>
      <Tooltip contents="Top-left tooltip!!" position="topLeft">
        <div class="red"></div>
      </Tooltip>
      <Tooltip contents="Top-right tooltip!" position="topRight">
        <div class="blue"></div>
      </Tooltip>
      <Tooltip contents="Calculated tooltip!">
        <div class="blue"></div>
      </Tooltip>
      <Tooltip contents="Right tooltip!" position="right">
        <div class="green"></div>
      </Tooltip>
      <Tooltip contents="Down tooltip!" position="down">
        <div class="orange"></div>
      </Tooltip>
      <Tooltip contents="Calculated tooltip!">
        <div class="red"></div>
      </Tooltip>

    </div>
  </header>
</template>

<style scoped>
header {
  line-height: 1.5;
  position: relative;
  z-index: 0;
}

@media (min-width: 1024px) {
  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>


