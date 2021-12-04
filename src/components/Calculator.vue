<template>
  <div>Tip Calculator</div>
  <div class="card">
    <div class="form-card">
      <label>Bill</label>
      <br />
      <input
        class="numInput"
        type="number"
        v-model="bill"
        placeholder="0"
        required
      />
      <br />
      <label>Select Tip %</label>
      <div class="grid">
        <input type="button" value="5%" />
        <input type="button" value="10%" />
        <input type="button" value="15%" />
        <input type="button" value="25%" />
        <input type="button" value="50%" />
        <input
          class="custom-btn"
          type="number"
          v-model="custom"
          placeholder="custom"
        />
      </div>
      <br />
      <label>Number of People</label>
      <br />
      <input
        class="numInput"
        type="number"
        v-model="people"
        placeholder="0"
        required
      />
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
  data() {
    return {
      bill: null,
      people: null,
      custom: null,
    };
  },
};
</script>

<style scoped>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  border-radius: 5px;
  width: 50%;
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

.custom-btn {
  background-color: hsl(189, 41%, 97%);
  border: hsl(183, 100%, 15%);
  border-radius: 3px;
  color: hsl(183, 100%, 15%);
  padding: 5px 10px;
  width: 50px;
  margin: 0;
  text-align: center;
}

.numInput {
  margin-bottom: 20px;
  text-align: right;
  background-color: hsl(189, 41%, 97%);
  border: hsl(189, 41%, 97%);
  border-radius: 3px;
  padding: 5px 20px;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
}
</style>
