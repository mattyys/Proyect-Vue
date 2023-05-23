<template>
    <main>
        <h1>Stiema de Control de Gastos</h1>
        <section id="section-info">
            <div class="button-list-container">
                <button class="info-button list" v-on:click="estado = true">Lista de Gastos</button>
                <button class="info-button pay" v-on:click="estado = false">Pagadas</button>
            </div>
            <div class="ingreso-gastos-container">

                <input class="add-info-text" type="date" name="dateCosto" id="dateCosto" v-model="nuevaFecha">
                <input class="add-info-text" type="text" placeholder="Ingrese Detalle" v-model="nuevoGasto">
                <input class="add-info-text" type="number" placeholder="Importe" v-model="nuevoCosto">
                <button class="primary add-button" v-on:click="addGasto">Agregar Gasto</button>

            </div>

            <div class="gastos-container"  v-for="(gasto, index) in detallesGastos" :key="index">

                <div class="info-gastos" v-if="estado ? !gasto.pago : gasto.pago">
                    <h4>Fecha {{ gasto.fecha }} </h4>
                    <h4>Detalle: {{ gasto.detalle }} </h4>
                    <h4 style="color: red;"> Importe: ${{ gasto.costo }}</h4>
                    <button class="primary pay-button" v-on:click="pagar(gasto)">{{ gasto.pago ? 'Deshacer' :
                        'Pagar' }}</button>
                </div>
            </div>
            <div>
                <h3  class="resumen">Total: $ {{ totalCostosGastos }} </h3>
            </div>


        </section>
    </main>
</template>




<script>


export default {
    name: "ControlGastos",
    data() {
        return {
            title: "Control de Gastos",
            estado: true,//indica cuando es un nuevo gasto agregado en true
            nuevoGasto: '',//ingreso detalle del gasto
            nuevoCosto: 0,//ingreso del importe del gasto
            nuevaFecha: new Date().toISOString().substring(0, 10),//devuelve la fecha actual
            conIva: false,
            IVA: 1.22,
            contador: 1,
            detallesGastos: [ //coleccion de gastos
                /*  {
                      id: 0,
                      detalle: 'Prueba',
                      costo: 100,
                      pago: false,
                      fecha: datetime.now
                      sumaIva:false
                  },*/

            ]
        }
    },

    methods: {
        addGasto: function () { //confirma que los campos no esten vacios y agrega a la coleccion
            if (this.nuevoCosto === 0) {
                return confirm("Ingrese un Importe");
            } else if (this.nuevoGasto === '') {
                confirm("Ingrese un detalle del gasto");
            } else {
                this.detallesGastos.push(
                    {
                        id: this.detallesGastos.length ? this.detallesGastos.length : 0,
                        detalle: this.nuevoGasto.toUpperCase(),
                        costo: this.nuevoCosto,
                        pago: false,
                        fecha: this.nuevaFecha,
                        sumaIva: this.conIva
                    }
                )
            }
        },
        itemMasIva: function (costo) {
            return costo * this.IVA;
        },
        pagar: function (gasto) {//cambia el estado del pago o pendiente
            if (gasto.pago) {
                gasto.pago = false;
            } else {
                gasto.pago = true;
            }
        }
    },

    computed: {
        totalCostosGastos: function () {//realiza la suma de la lista de pagos o pendientes
            let sumaP = 0;
            let sumaG = 0;

            for (let i = 0; i < this.detallesGastos.length; i++) {
                if (this.detallesGastos[i].pago == false) {
                    sumaG += this.detallesGastos[i].costo;
                } else {
                    sumaP += this.detallesGastos[i].costo;
                }
            }
            if (this.estado) {
                return sumaG;
            } else {
                return sumaP;
            }
        }
        


    }
}
</script>




<style scoped>
section {
    margin: 35px;
    border-width: 0.5px;
    border-style: dashed;
    border-radius: 30px 30px 0 0;
}

h1 {
    text-align: center;
}

h3 {
    color: rgb(28, 27, 27);
    font-size: x-large;
    padding: 5px;
    margin: auto;

}


.primary {
    height: 30px;
    padding-left: 24px;
    padding-right: 24px;
    border-radius: 10px;
    cursor: pointer;
    font-weight: 500;
    margin: 5px;
    background-color: #6750A4;
    color: #FFFFFF;
}

.info-button {
    height: 30px;
    padding: 0 24px 0;
    width: 50%;
    color: rgb(41, 41, 41);
    font-weight: 700;
    font-size: large;

}
.list{
    border-radius: 30px 0 0 0;
   
    background-color: rgb(118, 235, 190);
}

.pay {
    border-radius: 0 30px 0 0;
   
    background-color: rgb(135, 171, 255);
}

.primary:hover {
    background-color: #735EAB;
    box-shadow: 0px 0px 4px 0px rgba(0, 0, 0, 0.50);
}

.primary:active {
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

.info-gastos {
    display: flex;
    align-items: center;
    justify-content: center;
    justify-content: space-evenly;
}

.ingreso-gastos-container {
    display: flex;
    justify-content: center;
    align-items: center;
    justify-content: space-around;
    border: solid 0.5px #494949;
}
.pay-button{
    background-color: rgb(86, 91, 89);
}
.pay-button:hover{
    background-color: #a7a6a6;
    box-shadow: 0px 0px 4px 0px rgba(0, 0, 0, 0.50);
}
.add-info-text{
    width: 25%;
    height: auto;
    font-size: large;
}
</style>