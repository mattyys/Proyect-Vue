<template>
    <h1 v-if="estado">Soy el sistema de tareas</h1>
    <!--el v-if es el uso del condicional if que puede tomar el valor devuelto en una funcion-->
    {{ hola }}
    <button v-on:click="estado = !estado">
        {{ estado ? 'desaparece' : 'aparece' }}</button>

    <button v-on:click="hecho = true">Pendientes</button>

    <button v-on:click="hecho = false">Para hacer</button>

    <button v-on:click="dadoBaja = true">Baja Tarea</button>



    <div v-for="(tar, index) in tareas" :key="index">
        <div class="cuadro-tareas" v-if="hecho ? !tar.estado : tar.estado">
            {{ tar.tarea }}

            <button v-on:click="tar.estado = !tar.estado">{{ hecho ? 'Realizada' : 'reanudar' }}
            </button>

            <button v-on:click="eliminar(index)">ELiminar tarea</button>

            <button v-on:click="tar.baja = !tar.baja">{{ tar.baja ? 'Alta Tarea' : 'Baja Tarea' }}</button>
        </div>
    </div>

    <input type="text" v-model="nuevaTarea"><!--con v-model se utiliza el texto ingresado-->

    <button v-on:click='cargar'>Crear tarea {{ sumar }}</button>

    <button v-on:click="sumar"></button>

    <button v-on:click.right.prevent="console.log('boton derecho')"
        v-on:click.left.prevent="console.log('boton izquierdo')">
        probando
    </button>
</template>

<script>
export default {
    name: "TaskComponent",
    data() {
        return {
            hola: "hola componente",
            estado: true,
            hecho: true,
            numero: 1,
            nuevaTarea: '',
            tareas: [
                {
                    id: 0,
                    tarea: "algo para hacer 1",
                    realizado: false,
                    baja: false,
                    costo: 12
                },
                {
                    id: 1,
                    tarea: "algo para hacer 2",
                    realizado: false,
                    baja: false,
                    costo: 15
                },
                {
                    id: 2,
                    tarea: "algo para hacer 3",
                    realizado: false,
                    baja: false,
                    costo: 10
                },
            ]

        }
    },
    methods: {
        cargar: function () {
            this.tareas.push({
                id: this.tareas.length ? this.tareas.length : 0,
                tarea: this.nuevaTarea,
                realizado: false
            })
        },
        eliminar: function (index) {
            if (confirm("Eliminar Tarea?")) {
                this.tareas.splice(index, 1)
            }

        }
    },
    computed: {
        sumar: function () {
            return this.numero + this.numero + 1
        },
        carrito: function () {
            let sumando = 0;
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
        console.log("beforecreate")
    },
    created() {
        console.log("created")
    },
    beforeMount() {
        console.log("beforemount")
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
.cuadro-tareas {
    margin-top: 14px;
    border: solid 1px black;
    background: aquamarine;
    height: auto;
    width: aut;
}

button {
    margin: 4px
}
</style>