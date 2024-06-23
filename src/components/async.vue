<script setup>
import { ref } from "vue";

const carpetas = ref([{ "name": "Carpeta" }, { "name": "Carpeta" }, { "name": "Carpeta" }]);
const subcarpetas = ref([
    [{ "name": "Subcarpeta" }, { "name": "Subcarpeta" }, { "name": "Subcarpeta" }],
    [{ "name": "Subcarpeta" }, { "name": "Subcarpeta" }, { "name": "Subcarpeta" }],
    [{ "name": "Subcarpeta" }, { "name": "Subcarpeta" }, { "name": "Subcarpeta" }]
]);

const pan = [ref(true), ref(true), ref(true)];
const indice = ref(-1);
const dos = ref(-1);
let nombre;

function cambiarIndex(index) {
    if (indice.value == index) {
        indice.value = -1;
    } else {
        indice.value = index;
    }
}

function añadirCar() {
    nombre = prompt("Ingrese el nombre de la carpeta");
    let uno = { "name": nombre };
    carpetas.value.push(uno);
    subcarpetas.value.push([]); // Añadir una nueva submatriz vacía para la nueva carpeta
}

function añadirSub(i) {
    nombre = prompt("Ingrese el nombre de la subcarpeta");
    let uno = { "name": nombre };
    subcarpetas.value[i].push(uno);
}
</script>

<template>
<div class="bg-slate-300 w-80">
    <div class="items-center mb-1 flex" v-for="(car, i) in carpetas" :key="i" @click="cambiarIndex(i)">
        <div>
            <p class="rounded m-2 p-3 flex justify-center">📁{{ car.name + " " + (i + 1) }}</p>

            <div class="items-center mb-1 flex justify-evenly rounded p-1 ml-5" v-if="i == indice" v-for="(sub, j) in subcarpetas[i]" :key="j">
                <div class="rounded p-2 ml-20">
                    <p>📁{{ sub.name + " " + (j + 1) }}</p>
                </div>
            </div>

        </div>
        <div>
            <button class="flex justify-center items-center bg-blue-300 rounded-lg border h-9 w-10 border-black" @click.stop="añadirSub(i)">Add</button>
        </div>
    </div>
    <div class="items-center mb-1 flex space-x-4 p-2">
        <p>Añadir Carpetas</p>
        <button class="flex justify-center items-center bg-blue-300 rounded-lg border h-9 w-10 border-black" @click="añadirCar()">Add</button>
    </div>
</div>
</template>
