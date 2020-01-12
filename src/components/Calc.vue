<template>
  <div class="hello">
    <h2>Calculadora de passageiros</h2>
    
    <div class="form">
      <div>
        <label for='payers'>Nr Pagantes</label>
        <input id="payers" type="number" v-model="payers" placeholder="0" @change="updateInput">
      </div>
      <div>
        <label for='children'>Nr Crianças</label>
        <input id="children" type="number" v-model="children" placeholder="0" @change="updateInput">
      </div>
      <div>
        <label for='free'>Nr Cortesias</label>
        <input id="free" type="number" v-model="free" placeholder="0" @change="updateInput">
      </div>
      <div>
        <label for='amountPaid'>Valor de voucher pago</label>
        <input id="amountPaid" type="number" v-model="amountPaid" placeholder="0" @change="updateInput">
      </div> 
      <div>
        <label for='isCc'>Cartão</label>
        <input id="isCc" type="checkbox" v-model="isCc" @change="updateInput">
      </div> 
    </div>

    <div>
      <h3>Resumo</h3>
      <p>Total de pessoas: {{ total }}</p>
      <p>Preço do ingresso: R$ {{ ticketPrice }}</p>
      <p>À pagar: R$ {{ debit }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: () => ({
    payers: 0,
    children: 0,
    free: 0,
    amountPaid: 0,
    isCc: false,
    total: 0,
    debit: 0,
    ticketPrice: 0,
  }),
  methods: {
    updateInput: function () {
      this.payers = parseInt(this.payers || 0);
      this.children = parseInt(this.children || 0);
      this.free = parseInt(this.free || 0);

      this.total = this.payers + this.children + this.free;
      
      this.ticketPrice = 80;

      if (this.isCc) {
        this.ticketPrice += 5;
      }

      if (this.total >= 20) {
        this.ticketPrice -= 10;
      }

      this.debit = (this.ticketPrice * this.payers) - this.amountPaid;

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.form {
  display: flex;
  flex-flow: column wrap;
  align-content: center;
}
label {
  height: 50px;
  text-align: right;
}
input {
  font-size: 20px;
  height: 25px;
  width: 50px;
  padding: 5px;
  margin-top: 15px;
  box-sizing: border-box;
}
</style>
