<template>
  <div class="wrapper">
    <div class="dialog">
      <div class="header">
        <div class="title">Models</div>
        <div class="close-btn">&times;</div>
      </div>
      <div class="filter">
        <input type="checkbox"><span>All</span><input type="text"><button>Search</button>
      </div>
      <div class="item-container">
        <div class="item">
          <input type="checkbox">
          <div>IPN</div>
        </div>
      </div>
      <div class="actions"></div>
    </div>
  </div>
</template>

<script>
export default {
}
</script>

<style scoped>
.wrapper {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100vw;
  background-color: rgba(0, 0, 0, 0.25)
}
</style>
