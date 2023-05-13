<template>
    <h1 v-if="estado">Soy el sistema de tareas</h1><!--el v-if es el uso del condicional if que puede tomar el valor devuelto en una funcion-->
    {{ hola }}
    <button v-on:click="estado = !estado">
        {{ estado ? 'desaparece' : 'aparece' }}</button>
    <button v-on:click="hecho = true">Realizadas</button>
    <button v-on:click="hecho = false">Para hacer</button>



    <div v-for="(tar, index) in tareas" :key="index">
        <div class="cuadro-tareas" v-if="hecho ? !tar.estado : tar.estado">
            {{ tar.tarea }}
            <button v-on:click="tar.estado = !tar.estado">{{ hecho ? 'Realizada' : 'reanudar' }}
            </button> 
            <button v-on:click="eliminar(index)">ELiminar tarea</button>  
        </div>
    </div>
    <input type="text" v-model="nuevaTarea"><!--con v-model se utiliza el texto ingresado-->
    <button v-on:click = 'cargar'>Crear tarea</button>
    
</template>

<script>
export default {
    name: "TaskComponent",
    data() {
        return {
            hola: "hola componente",
            estado: true,
            hecho: true,
            nuevaTarea: '',
            tareas: [
                {
                    id: 0,
                    tarea: "algo para hacer 1",
                    realizado: false
                },
                {
                    id: 1,
                    tarea: "algo para hacer 2",
                    realizado: false
                },
                {
                    id: 2,
                    tarea: "algo para hacer 3",
                    realizado: false
                },
            ]

        }
    },
    methods: {
        cargar:function (){
            this.tareas.push({
                id : this.tareas.length ? this.tareas.length : 0,
                tarea : this.nuevaTarea,
                realizado: false
            })
        },
        eliminar:function(index){
            if (confirm("Eliminar Tarea?")){
                this.tareas.splice(index, 1)
            }
             
        }
    },


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