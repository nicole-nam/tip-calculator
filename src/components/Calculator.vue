<template>
  <div>Tip Calculator</div>
  <div class="card">
    <div class="form-card">
      <label>Bill</label>
      <br />
      <img class="icon" src="../assets/icon-dollar.svg" />
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
        <div v-for="amount in amounts" :key="amount.index">
          <input
            v-if="amount.text == 'amount'"
            class="custom-btn"
            :placeholder="amount.value"
            @click="selected(amount.index)"
            type="number"
            required
          />
          <input
            v-else
            type="button"
            :class="{ active: amount.isActive, notActive: !amount.isActive }"
            @click="selected(amount.index, amount.value)"
            :value="amount.text"
          />
        </div>
      </div>
      <br />
      <label>Number of People</label>
      <br />
      <img class="icon" src="../assets/icon-person.svg" />
      <input
        class="numInput"
        type="number"
        v-model="people"
        placeholder="0"
        v-on:keyup="tipAmount"
        required
      />
    </div>
    <div class="tip-card">
      <div class="margin-bottom flex">
        <div>
          <p>Tip Amount</p>
          <p>/person</p>
        </div>
        <div class="totalAmount" v-if="this.tipPerPerson !== undefined">
          $ {{ tipPerPerson }}
        </div>
      </div>
      <div class="flex">
        <div>
          <p>Total</p>
          <p>/person</p>
        </div>
        <div class="totalAmount" v-if="this.totalPerPerson !== undefined">
          $ {{ totalPerPerson }}
        </div>
      </div>
      <button class="resetBtn" @click="reset()">Reset</button>
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
      custom: "Custom",
      tipPerPerson: "0.00",
      totalPerPerson: "0.00",
      tipSelected: null,
      amounts: [
        {
          index: 0,
          value: 5,
          text: "5%",
          isActive: false,
        },
        {
          index: 1,
          value: 10,
          text: "10%",
          isActive: false,
        },
        {
          index: 2,
          value: 15,
          text: "15%",
          isActive: false,
        },
        {
          index: 3,
          value: 25,
          text: "25%",
          isActive: false,
        },
        {
          index: 4,
          value: 50,
          text: "50%",
          isActive: false,
        },
        {
          index: 5,
          value: "custom",
          text: "amount",
          isActive: false,
        },
      ],
    };
  },
  methods: {
    reset() {
      this.bill = null;
      this.people = null;
      this.custom = "Custom";
      this.tipPerPerson = "0.00";
      this.totalPerPerson = "0.00";
      this.tipSelected = null;
      for (let i = 0; i < this.amounts.length; i++) {
        this.amounts[i].isActive = false;
      }
    },
    selected(t, v) {
      this.tipSelected = v;
      for (let i = 0; i < this.amounts.length; i++) {
        if (this.amounts[i].index == t) {
          this.amounts[i].isActive = true;
        } else {
          this.amounts[i].isActive = false;
        }
      }
    },
    tipAmount() {
      var tipAmount = this.tipSelected / 100;
      var perPerson = (this.bill * tipAmount) / this.people;
      this.tipPerPerson = ((this.bill * tipAmount) / this.people).toFixed(2);
      this.totalPerPerson = (this.bill / this.people + perPerson).toFixed(2);
    },
  },
};
</script>

<style scoped>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  background-color: #fff;
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

.flex {
  display: flex;
  justify-content: space-between;
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

.icon {
  position: absolute;
  padding: 5px;
}

.active {
  background-color: hsl(184, 14%, 56%);
  border: hsl(184, 14%, 56%);
  border-radius: 3px;
  color: hsl(183, 100%, 15%);
  padding: 5px 10px;
  width: 100%;
}

.notActive {
  background-color: hsl(183, 100%, 15%);
  border: hsl(183, 100%, 15%);
  border-radius: 3px;
  color: #fff;
  padding: 5px 10px;
  width: 100%;
}

.totalAmount {
  color: hsl(185, 41%, 84%);
}
</style>
