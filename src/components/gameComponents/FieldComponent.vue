<script setup>

</script>

<template>

</template>

<style scoped>
.game {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.popover {
  --bs-popover-max-width: 500px;
  --bs-popover-header-bg: #9f4045;
  --bs-popover-header-color: white;
}

.popover-table td {
  height: 45px;
  border: 1px solid black;
  text-align: center;
  color: black;
  width: 45px;
}

.popover-table img {
  height: 100%;
}

.popover-table span {
  font-size: 30px;
}

.popover-table div {
  font-size: 20px;
  font-weight: bolder;
}

.popover .popover-arrow:after {
  border-top-color: #9f4045;
  border-bottom-color: #9f4045;
}
</style>
