<template>
  <div class="modal">
    <h1>
      Demo fonctionnement composition API with ref
    </h1>
    <p>
      Name : {{ personOne.name}} , age: {{ personOne.age }}
    </p>
    <button @click="handleClick">
      Fonction in setup()
    </button>
    <input type="text" v-model="personOne.name">
    <h1>Reactive</h1>
    <p>
      Name : {{ personTwo.name}} , age: {{ personTwo.age }}
    </p>
    <button @click="updateWithReactive">
      Update With reactive
    </button>
    <p>L'age total est de : {{ totalAge }} </p>
  </div>

</template>

<script>
import {ref, reactive, computed} from "@vue/reactivity";

export default {
  // pour la composition API: ajout d'une méthode setup: Elle est lancé avant toutes les autres
  // ref permet de rendre réactif les données simple
  // reactive marche qu'avec les objects
  name: 'DemoCompositionApi',
  setup() {
    //ref permet de rendre les variables réactive
    const personOne = reactive({ name: 'Mario' , age: 30 });
    const personTwo = reactive({ name: 'Luigi' , age : 35 })

    const totalAge= computed( () => {
      return personOne.age + personTwo.age
    })

    const handleClick = () => {
      personOne.value.name = 'luigi'
      console.log('you clicked me')
    }

    const updateWithReactive = () => {
      personTwo.name = 'Julien'
      console.log('you clicked me')
    }

    return {
      personOne: personOne,
      personTwo: personTwo,
      totalAge: totalAge,
      handleClick : handleClick,
      updateWithReactive : updateWithReactive
    }
  } ,
  created() {
    console.log('created')
  },
  mounted() {
    console.log('mounted')
  },

  methods :{
    closeModal() {
      this.$emit('close')
    }
  }

}
</script>

<style scoped>
.modal  {
  width: 400px;
  padding: 20px;
  margin: 100px auto;
  background: white;
  border-radius: 10px;
}
.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0,0,0,0.5);
  width: 100%;
  height: 100%;
}
.modal h1 {
  color: #03cfb4;
  border:none;
  padding: 0;
}

</style>