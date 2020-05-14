<template>
  <div class="calculadora" onselectstart="return false">
    <div class="resultado">{{resultado}}</div>
    <div @click="borrar()" class="btn oscuro">C</div>
    <div @click="signo()" class="btn oscuro">+/-</div>
    <div @click="porcentaje()" class="btn oscuro">%</div>
    <div @click="dividir()" class="btn operador">/</div>
    <div @click="agregar(7)" class="btn">7</div>
    <div @click="agregar(8)" class="btn">8</div>
    <div @click="agregar(9)" class="btn">9</div>
    <div @click="multiplicar()" class="btn operador">*</div>
    <div @click="agregar(4)" class="btn">4</div>
    <div @click="agregar(5)" class="btn">5</div>
    <div @click="agregar(6)" class="btn">6</div>
    <div @click="restar()" class="btn operador">-</div>
    <div @click="agregar(1)" class="btn">1</div>
    <div @click="agregar(2)" class="btn">2</div>
    <div @click="agregar(3)" class="btn">3</div>
    <div @click="sumar()" class="btn operador">+</div>
    <div @click="agregar(0)" class="btn cero btn-abajo">0</div>
    <div @click="puntoDecimal()" class="btn btn-abajo">.</div>
    <div @click="igual()" class="btn operador btn-abajo">=</div>
  </div>
</template>

<script>
export default {
  name: "calculadora",
  data() {
    return {
      resultado: 0,
      operadorClick: false,
      operador: null,
      anterior: null,
      puntito: false
    };
  },
  methods: {
    borrar() {
      this.resultado = 0;
    },
    signo() {
      this.resultado =
        this.resultado < 0
          ? (this.resultado = this.resultado - this.resultado * 2)
          : (this.resultado = this.resultado - this.resultado * 2);
    },
    porcentaje() {
      this.resultado = this.resultado / 100;
    },
    agregar(numero) {
      if (this.operadorClick && !this.puntito) {
        this.resultado = numero;
        this.operadorClick = false;
      } else {
        if (this.operadorClick && this.puntito) {
          this.resultado = "" + this.resultado + numero;
          this.puntito = false;
          this.operadorClick = false;
        } else {
          this.resultado =
            this.resultado === 0
              ? (this.resultado = numero)
              : "" + this.resultado + numero;
        }
      }
    },
    puntoDecimal() {
      if (this.operadorClick) {
        this.resultado = "0.";
        this.puntito = true;
      }
      if (/\d+\.+/g.test(this.resultado)) {
      } else {
        this.resultado = this.resultado + ".";
      }
    },
    dividir() {
      this.operador = (a, b) => a / b;
      this.anterior = this.resultado;
      this.operadorClick = true;
    },
    multiplicar() {
      this.operador = (a, b) => a * b;
      this.anterior = this.resultado;
      this.operadorClick = true;
    },
    restar() {
      this.operador = (a, b) => a - b;
      this.anterior = this.resultado;
      this.operadorClick = true;
    },
    sumar() {
      this.operador = (a, b) => a + b;
      this.anterior = this.resultado;
      this.operadorClick = true;
    },
    igual() {
      this.resultado = this.operador(
        Number(this.anterior),
        Number(this.resultado)
      );
      this.anterior = null;
      this.operadorClick = true;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculadora {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 0;
  width: 100vw;
  height: calc(100vh - 56px);
  vertical-align: middle;
  font-size: 1.5rem;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

div {
  display: flex;
  justify-content: center;
  align-items: center;
}

.resultado {
  justify-content: flex-end;
  width: 100vw;
  height: calc(((100vh - 56px) / 7) * 2);
  color: white;
  padding-right: 1rem;
}

.btn {
  cursor: pointer;
  margin: 0px;
  padding: 0px;
  width: calc(100vw / 4);
  height: calc((100vh - 56px) / 7);
  color: #2b3e4e;
  background-color: #d4d4d2;
}

.btn:active {
  background-color: yellow;
}

.cero {
  width: calc((100vw / 4) * 2);
}

.oscuro {
  color: white;
  background-color: #424345;
}

.operador {
  color: white;
  background-color: #f79c51;
}
</style>
