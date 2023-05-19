<template>
    <h1 v-if="estado">soy el sistema de tareas</h1>
    <button v-on:click="estado = !estado"> {{ estado ? "desaparece" : "aparece" }} </button>
    {{ hola }}
    <button v-on:click="hecho = true">realizadas</button>
    <button v-on:click="hecho = false">Para hacer</button>
    
    <div v-for="(tar, index) in tareas" :key="index">
        <div class="cuadrado" v-if="hecho ? !tar.estado : tar.estado">
            {{ tar.tarea }}
            <button v-on:click="tar.estado = !tar.estado">
                {{ hecho ? 'realizada' : "reanudar" }}
            </button>
        </div>
    </div>

    <input type="text" v-model='nuevaTarea'>
    <button v-on:click='cargar'> Crear Tarea </button>
</template>

<script>
export default {
    name: "TasksComponent",
    data() {
        return {
            hola: "hola como andas",
            estado: false,
            hecho: true,
            nuevaTarea: '',
            tareas: [{
                id: 0,
                tarea: "algo para hacer",
                realizado: false,
            },
            {
                id: 1,
                tarea: "algo para hacer",
                realizado: false,
            },
            {
                id: 2,
                tarea: "algo para hacer",
                realizado: false,
            },
            ],
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