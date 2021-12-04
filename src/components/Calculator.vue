<template>
  <div>Tip Calculator</div>
  <div class="card">
    <label>Bill</label>
    <br />
    <input type="number" />
    <br />
    <label>Select Tip %</label>
    <div class="grid">
      <input type="button" value="5%" />
      <input type="button" value="10%" />
      <input type="button" value="15%" />
      <input type="button" value="25%" />
      <input type="button" value="50%" />
      <input type="button" value="Custom" />
    </div>
    <br />
    <label>Number of People</label>
    <input type="number" />
  </div>
</template>

<script>
export default {
  name: "Calculator",
  props: {},
};
</script>

<style scoped>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  border-radius: 5px;
  width: 40%;
  margin: 100px auto;
}
.grid {
  display: grid;
  grid-gap: 1px;
  grid-template-columns: repeat(3, 1fr);
}
</style>
