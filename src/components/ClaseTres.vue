<template>
    <h1 v-if="numero === 1">1</h1>
    <h1 v-else-if="numero === 2">2</h1>
    <h1 v-else>numero grande</h1>
    <button v-on:click="estado = !estado">
        {{ estado ? "desaparece" : "aparece" }}
    </button>
    {{ hola }}

    <button v-on:click="hecho = true">realizadas</button>
    <button v-on:click="hecho = false">Para hacer</button>

    <div v-for="(tar, index) in tareas" :key="index">
        <div class="cuadrado" v-if="hecho ? !tar.estado : tar.estado">
            {{ tar.tarea }} costo: {{ tar.costo }}
            <button v-on:click="tar.estado = !tar.estado">
                {{ hecho ? 'realizada' : "reanudar" }}
            </button>
        </div>
    </div>


    <input type="text" v-model='nuevaTarea'>
    <button v-on:click='cargar'>
        Crear Tarea {{ sumar }}
    </button>

    <button v-on:click.right.prevent="boton = 'bandera'" v-on:click.left.prevent="boton = 'bomba'">
        {{ boton }}
    </button>

    <button v-on:click="numero = numero + 1">
        sumar uno
    </button>
    {{ numero }} total {{ carrito }} / mas IVA {{ masIva }}
</template>
  
<script>
export default {
    name: "ClaseTres",
    data() {
        return {
            hola: "hola como andas",
            estado: false,
            hecho: true,
            numero: 1,
            nuevaTarea: '',
            boton: "nada",
            tareas: [
                {
                    id: 0,
                    tarea: "arroz",
                    realizado: false,
                    costo: 5
                },
                {
                    id: 1,
                    tarea: "papas",
                    realizado: false,
                    costo: 5
                },
                {
                    id: 2,
                    tarea: "polenta",
                    realizado: false,
                    costo: 50
                },
            ]
        };
    },

    methods: {
        cargar: function () {
            this.tareas.push({
                id: this.tareas.length ? this.tareas.length : 0,
                tarea: this.nuevaTarea,
                estado: false,
            });
        }
    },
    computed: {
        sumar: function () {
            return this.numero + 10
        },
        carrito: function () {
            let sumando = 0
            for (let index = 0; index < this.tareas.length; index++) {
                sumando = sumando + this.tareas[index].costo
            }
            return sumando
        },
        masIva: function () {
            return this.carrito * 1.22
        }
    },

    beforeCreate() {
        console.log("beforeCreate")
    },
    created() {
        console.log("cteated")
    },
    beforeMount() {
        console.log("beforeMount")
    },
    mounted() {
        console.log("mounted")
    },
    beforeUpdate() {
        console.log("beforeupdate")
    },
    updated() {
        console.log("updated")
    }
}
</script>
  
<style scoped>
.cuadrado {
    border: solid 2px black;
    padding: 10px;
    margin: 5px;
}
</style>