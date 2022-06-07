<template>
  <div class="info">
    <div class="form-group">
      <label>Укажите год:
        <input v-model="year"/>
      </label>
    </div>
    <div class="form-group">
      <label>Укажите ставку дисконтирования:
        <input v-model="percent">
      </label>
    </div>
      <button @click="calculateNPV" type="submit">Подсчитать NPV</button>

    <div class="display-result">
      <p>NPV по {{year}} год: {{result}}</p>
    </div>
  </div>
</template>

<script>

import axios from "axios";
export default {
  name: 'HelloWorld',
  data() {
    return {
      year: 2050,
      percent: 0.2,
      result: null,
    }
  },
  methods: {
    calculateNPV: async function() {
     await axios
          .post('http://127.0.0.1:8000/calculate/', {
              year: this.year,
              percent: this.percent,
              })
          .then(response => {
            this.result = response.data
          })
          .catch(error => {
            this.result = error.response.data.detail[0].msg;
          });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-group{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-flow: column wrap;
  padding: 10px;
}
.info {
  border: darkcyan 3px solid;
  border-radius: 20px;
  margin: 0 20% 0 20%;
  padding-top: 20px;
}
p {
  color: red;
}
</style>
