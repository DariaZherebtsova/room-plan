<template>
  <div class='legend'>
    <div class='legend-item'>
      <div class='legend-item__color'></div>
      <div class='legend-item__label'>Front-end</div>
      <div class='legend-item__counter'>5</div>
    </div>
  </div>
</template>

<script>
// import legend from "@/assets/data/legend.json";

export default {

}
</script>

<style scoped>
.legend {
  border-left: 1px solid goldenrod;
  padding: 30px 20px;
}
.legend-item {
  display: grid;
  grid-template-columns: 30px 1fr 30px;
}
.legend-item__color {
  width: 15px;
  height: 15px;
  border-radius: 4px;
  background-color: aquamarine;
}
.legend-item__counter {
  color: grey;
}

</style>