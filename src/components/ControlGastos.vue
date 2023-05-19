<template>
    <h1>Control de Gastos</h1>
    <section>

        <button v-on:click="estado = true">Lista de Gastos</button>
        <button v-on:click="estado = false">Pagadas</button>

        <div class="gastos-container" v-for="(gasto, index) in detallesGastos" :key="index">
            
            <div class="info-gastos" v-if="estado ? !gasto.pago : gasto.pago">
                <h3>{{ gasto.detalle }} <span style="color: red;"> Costo: ${{ gasto.costo }}</span></h3>
                <h3>mas IVA {{ itemMasIva(gasto.costo) }}</h3>
                <button v-on:click="gasto.pago = true">Pagar</button>
            </div>

        </div>
        <div class="ingreso-gastos-container">
            <input type="text" v-model="nuevoGasto">
            <input type="number" v-model="nuevoCosto">
            <button v-on:click="addGasto">Agregar Gasto</button>
        </div>

    </section>
</template>




<script>
export default {
    name: "ControlGastos",
    data() {
        return {
            title: "Control de Gastos",
            estado: true,//indica cuando es un nuevo gasto agregado en true
            nuevoGasto: '',
            nuevoCosto: 0,
            iva:1.22,
            contador: 1,
            totListGasto: 0,
            totListPagado: 0,
            detallesGastos: [
                {
                    id: 0,
                    detalle: 'Prueba',
                    costo: 100,
                    pago: false,
                },
              
            ]
        }
    },

    methods: {
        addGasto: function () {
            this.detallesGastos.push(
                {
                    id: this.detallesGastos.length ? this.detallesGastos.length : 0,
                    detalle: this.nuevoGasto,
                    costo: this.nuevoCosto,
                    pago: false
                }
            )
        },
        itemMasIva:function(costo){
            return costo * this.iva;
        }
    },

    computed:{
        totalAPagar:function(){
            let suma = 0;
            for (let i = 0; i < this.detallesGastos.length; i++){
                suma += this.detallesGastos[i].costo;
            }
            return suma;
        }
    }
}
</script>




<style scoped>
h1 {
    text-align: center;
}
h3{
    color: black;
}

button {
    height: 30px;
    padding-left: 24px;
    padding-right: 24px;
    border-radius: 20px;
    cursor: pointer;
    font-weight: 500;
    margin: 5px;
    background-color: #6750A4;
    color: #FFFFFF;
}

button:hover {
    background-color: #735EAB;
    box-shadow: 0px 0px 4px 0px rgba(0, 0, 0, 0.50);
}

button:active {
    transform: scale(0.98);
    box-shadow: none;
}

.info-gastos {
    margin-top: 14px;
    border: solid 1px black;
    background: aquamarine;
    height: auto;
    width: auto;
}
.info-gastos{
    display: flex;
    align-items: center;
    justify-content: center;
    justify-content: space-evenly;
}
</style>