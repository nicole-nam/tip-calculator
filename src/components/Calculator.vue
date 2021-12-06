<template>
  <div>Tip Calculator</div>
  <div class="card">
    <div class="form-card">
      <div class="bill">
        <div class="zero">
          <label>Bill </label>
          <span v-if="bill == null">Can't be zero</span>
        </div>
        <img class="icon" src="../assets/icon-dollar.svg" />
        <input
          class="numInput"
          :class="{ numPeople: !bill, numInput: bill }"
          type="number"
          v-model="bill"
          placeholder="0"
          v-on:keyup="tipAmount"
          required
        />
        <br />
      </div>
      <div class="select-tip">
        <label>Select Tip %</label>
        <div class="grid">
          <div v-for="amount in amounts" :key="amount.index">
            <input
              v-if="amount.text == 'amount'"
              class="custom-btn"
              :placeholder="amount.value"
              v-model="custom"
              v-on:keyup="tipAmount"
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
      </div>
      <div>
        <div class="zero">
          <label>Number of People </label>
          <span v-if="people == null">Can't be zero</span>
        </div>
        <img class="icon" src="../assets/icon-person.svg" />
        <input
          :class="{ numPeople: !people, numInput: people }"
          type="number"
          v-model="people"
          placeholder="0"
          v-on:keyup="tipAmount"
          required
        />
      </div>
    </div>
    <div class="tip-card">
      <div class="margin-bottom flex">
        <div>
          <p class="bold-font">Tip Amount</p>
          <p class="light-font">/person</p>
        </div>
        <div class="totalAmount" v-if="this.tipPerPerson">
          $ {{ tipPerPerson }}
        </div>
      </div>
      <div class="flex">
        <div>
          <p class="bold-font">Total</p>
          <p class="light-font">/person</p>
        </div>
        <div class="totalAmount" v-if="this.totalPerPerson">
          $ {{ totalPerPerson }}
        </div>
      </div>
      <button
        v-if="disabled"
        :class="{ disable: disabled }"
        class="resetBtn"
        @click="reset()"
        disabled
      >
        Reset
      </button>
      <button v-else class="resetBtn" @click="reset()">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  props: {},
  data() {
    return {
      disabled: true,
      bill: null,
      people: null,
      custom: null,
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
      this.custom = null;
      this.tipPerPerson = "0.00";
      this.totalPerPerson = "0.00";
      this.tipSelected = null;
      this.disabled = true;
      for (let i = 0; i < this.amounts.length; i++) {
        this.amounts[i].isActive = false;
      }
    },
    selected(t, v) {
      this.custom = null;

      this.tipSelected = v;
      for (let i = 0; i < this.amounts.length; i++) {
        if (this.amounts[i].index == t) {
          this.amounts[i].isActive = true;
        } else {
          this.amounts[i].isActive = false;
        }
      }
      this.tipAmount();
    },
    tipAmount() {
      if (this.custom && this.bill && this.people) {
        var customTip = this.custom / 100;
        var per = (this.bill * customTip) / this.people;
        this.tipPerPerson = ((this.bill * customTip) / this.people).toFixed(2);
        this.totalPerPerson = (this.bill / this.people + per).toFixed(2);
        this.tipSelected = null;
        for (let i = 0; i < this.amounts.length; i++) {
          this.amounts[i].isActive = false;
        }
      } else if (this.bill && this.tipSelected && this.people) {
        var tipAmount = this.tipSelected / 100;
        var perPerson = (this.bill * tipAmount) / this.people;
        this.tipPerPerson = ((this.bill * tipAmount) / this.people).toFixed(2);
        this.totalPerPerson = (this.bill / this.people + perPerson).toFixed(2);
        this.custom = null;
      }
      this.disabled = false;
    },
  },
};
</script>

<style scoped>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  background-color: #fff;
  border-radius: 5px;
  width: 550px;
  margin: 100px auto;
  padding: 20px;
  text-align: left;
  display: flex;
  justify-content: space-between;
  gap: 30px;
}

.tip-card {
  background-color: hsl(183, 100%, 15%);
  border-radius: 5px;
  width: 50%;
  padding: 20px;
  text-align: left;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.form-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 50%;
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
  background-color: hsl(186, 42%, 59%);
  border: hsl(186, 42%, 59%);
  border-radius: 3px;
  color: hsl(183, 100%, 15%);
  cursor: pointer;
  padding: 7px;
}

.numInput {
  margin-bottom: 20px;
  text-align: right;
  background-color: hsl(189, 41%, 97%);
  border: #fff;
  border-radius: 3px;
  padding: 5px 20px;
  width: 80%;
  cursor: pointer;
}

.numPeople {
  margin-bottom: 20px;
  text-align: right;
  background-color: hsl(189, 41%, 97%);
  border: 1px solid rgb(255, 81, 0);
  border-radius: 3px;
  padding: 5px 20px;
  width: 80%;
  cursor: pointer;
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
  cursor: pointer;
  width: 100%;
}

.notActive {
  background-color: hsl(183, 100%, 15%);
  border: hsl(183, 100%, 15%);
  border-radius: 3px;
  color: #fff;
  padding: 5px 10px;
  cursor: pointer;
  width: 100%;
}

.custom-btn {
  background-color: hsl(189, 41%, 97%);
  border: hsl(183, 100%, 15%);
  border-radius: 3px;
  color: hsl(183, 100%, 15%);
  padding: 5px 10px;
  text-align: center;
  cursor: pointer;
  width: 75%;
}

.totalAmount {
  color: hsl(172, 67%, 45%);
  font-weight: 900;
}

.disable {
  background-color: hsl(186, 42%, 59%);
  opacity: 0.5;
  cursor: not-allowed;
}

.zero {
  color: rgb(255, 81, 0);
  font-size: 10px;
  display: flex;
  justify-content: space-between;
  margin-right: 10px;
}

.light-font {
  opacity: 0.5;
  font-size: 14px;
}

.bold-font {
  font-weight: 700;
}

label {
  font-size: 12px;
  color: hsl(184, 14%, 56%);
}
</style>
