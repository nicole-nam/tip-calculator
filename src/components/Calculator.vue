<template>
  <div>Tip Calculator</div>
  <div class="card">
    <div class="form-card">
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
    <div class="tip-card">
      <div class="margin-bottom">
        <p>Tip Amount</p>
        <p>/person</p>
      </div>
      <div>
        <p>Total</p>
        <p>/person</p>
      </div>
      <button class="resetBtn">Reset</button>
    </div>
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
  padding: 20px;
  text-align: left;
  display: flex;
  gap: 30px;
}
.tip-card {
  background-color: hsl(183, 100%, 15%);
  border-radius: 5px;
  width: 40%;
  margin: auto;
  padding: 20px;
  text-align: left;
}

p {
  color: #fff;
  margin: 0;
}

.margin-bottom {
  margin-bottom: 50px;
}

.grid {
  display: grid;
  grid-gap: 1px;
  grid-template-columns: repeat(3, 1fr);
}

.resetBtn {
  width: 100%;
  margin-top: 20px;
  background-color: hsl(186, 42%, 59%);
  border: hsl(186, 42%, 59%);
  border-radius: 3px;
  color: hsl(183, 100%, 15%);
}

input[type="button"] {
  background-color: hsl(183, 100%, 15%);
  border: hsl(183, 100%, 15%);
  border-radius: 3px;
  color: #fff;
  padding: 5px 10px;
}

input[type="number"] {
  margin-bottom: 20px;
}
</style>
