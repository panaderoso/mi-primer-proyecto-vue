
<script setup>
import {ref, computed} from "vue";

  const name = 'Viu Dinamico';
  const styleColor="color:blue";
  const arrayColores = ["red","blue","green"];
  const arrayFavoritos = ref([]);
  const activo = false;

  const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];

  const arrayFrutasObjeto = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
        },
    ];

    const objetoFruta = {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana"
        };

        const arrayFrutasStock = [
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        stock: 0,
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
        stock: 10,
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
        stock: 20,
    },
];

const handleClick = (message) =>{
  alert("me hiciste click = "+message);
}

const counter= ref(0);

const increment =() =>{
  counter.value++;
}

const decrement = () => { 
  counter.value--;
 }

 const reset = () => { 
  counter.value = 0;
  }

  const add = () => {
    arrayFavoritos.value.push(counter.value)
  }

  const bloquearBtnAdd = computed(() => {
    const numSearch = arrayFavoritos.value.find(num => num === counter.value)
    //if(numSearch===0) return true;
    //return numSearch ? true : false;
    return numSearch || numSearch ===0;
  })
//Computed
const classCounter = computed(() => {
  if(counter.value === 0){
    return 'neutral';
  }
  if(counter.value > 0){
    return 'positive';
  }
  if(counter.value < 0){
    return 'negative';
  }

  '<span class="closebtn" onclick="this.parentElement.style.display='+"'"+'none'+"'"+';">&times;</span>'
  
});

</script>

<template>
  <h1>Hola vue js {{name.toUpperCase()}}!</h1>

  <h2 :style="styleColor"> Soy azul</h2>

  <h3 :style="`color: ${arrayColores[2]}`"> Soy azul</h3>

  <h3>
    {{activo ? 'Estoy activo':'Estoy inactivo'}}
  </h3>

  <h3 v-if="activo"> Estoy Activo</h3>
  <h3 v-if="!activo"> Estoy Inactivo</h3>

  <h3 v-if="activo"> Estoy Activo</h3>
  <h3 v-else> Estoy Inactivo</h3>


  <h3 v-if="activo===true"> Estoy Activo</h3>
  <h3 v-else-if="activo===false"> Estoy Inactivo</h3>
  <h3 v-else> Estoy Inactivo</h3>

  <h3 v-show="activo===true"> Estoy Activo v-show</h3>

  <ul>
    <li v-for="fruta in arrayFrutas" 
        :key="fruta.index">
      {{index}} - {{fruta}}
    </li>
  </ul>

  <ul>
    <li v-for="fruta in arrayFrutasObjeto"
        :key="fruta.name">
        {{fruta.name}} - {{fruta.price}} - {{fruta.description}}
    </li>
  </ul>
<!-- objeto y sus propiedades-->
  <ul>
    <li v-for="(value, propiedad,index) in objetoFruta"
        :key="index">
        {{index}} - {{propiedad}} : {{value}}
    </li>
  </ul>

  <!--fruta stock > 0 -->

  <ul>
    <li v-for="item in arrayFrutasStock"
        :key="item.name">
        <span v-if="item.stock > 0">
          {{item.name}}
        </span>
       
    </li>
  </ul>

<!-- otra manera stock-->
  <ul>
    <template v-for="item in arrayFrutasStock" :key="item.name">
    <li v-if="item.stock > 0">
        
          {{item.name}}
      
    </li>
  </template>
  </ul>
<div class="container text-center mt-3">
  
  <!-- click -->
  <h1>Click</h1>
    <button v-on:click="handleClick('texto 1')"> Activame 1</button>

    <button @click="handleClick('texto 2')"> Activame 2</button>


  <!-- modificadores de eventos -->
  <h1>Modificadores de Eventos</h1>
  <button @click.left="handleClick('texto Left')"> Activame Left</button>
  <button @click.middle="handleClick('texto Middle')"> Activame Middle</button>
  <button @click.right.prevent="handleClick('texto Right')"> Activame Right</button>

  <div class="btn-group">
    <!-- ref y computed-->
    <h1 >ref y computed (reactividad) </h1>
    <h2 :class="classCounter">{{counter}}</h2>
    <button @click.left="increment" class="btn btn-success"> Aumentar</button>
    <button @click.left="decrement" class="btn btn-danger"> Disminuir</button>
    <button @click.left="reset" class="btn btn-secondary"> Reset</button>
    <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary"> Add</button>
  </div>
   
<br />
  {{arrayFavoritos}}
  <ul class="list-group">
    <li class="list-group-item"
        v-for="(num,index) in arrayFavoritos"
        :key="index"
        >
        {{num}}
    </li>
  </ul>
</div>

</template>


<style>
.positive{
  color:green;
}
.negative{
  color:red;
}
.neutral{
  color:black;
}
</style>