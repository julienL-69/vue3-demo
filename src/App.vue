<template>
  <h1>{{title}}</h1>

<!--  Example Modal simple: envoie des datas par props et event (call fonction d'un component) pour fermeture-->
  <p>Example de modal simple avec props et event</p>
  <div v-if="showModal">
    <Modal :header="header" :textModal="textModal" theme="sale" @close="toggleModal()" ></Modal>
  </div>
  <button @click="toggleModal()">
    Open Modal simple
  </button>


<!--  Example Modal avec SLOT: Permet d'envoyé un html différent dans la modal pour la rendre plsu rétulisable ( props aussi si on veut)-->
  <p>Show Modal With slot</p>
  <div v-if="showModalSlot">
    <ModalSlot :headerSlot="headerSlot" @close="toggleModalSlot()" >
<!--      titre send by props et html par slot -->
        <h1>{{ headerSlot }}</h1>
        <p>Et voila un html envoyé par slot au Component</p>
    </ModalSlot>
  </div>
  <button @click="toggleModalSlot()">
    Open Modal With Slot
  </button>

  <!-- Example de teleport: use to  + css selector to say where teleport the component -->
  <p>Example de modal simple teleporté ( dans une div class  modalsTeleport , cf public/index.html)</p>
  <teleport to=".modalsTeleport" v-if="showModalTeleport">
    <Modal :header="headerTeleport" :textModal="textModal" @close="toggleModalTeleport" ></Modal>
  </teleport>
  <button @click="toggleModalTeleport">
    Open Modal Teleport
  </button>


</template>



<script>
import Modal from './components/Modal.vue'
import ModalSlot from './components/ModalSlot.vue'

export default {
  name: 'App',
  components: {
    Modal , ModalSlot
  },
  data() {
    return {
      title : 'New feature Vue3',
      header : 'Modal simple example',
      headerSlot : 'Titre send by props',
      headerTeleport : 'Modal teleporté dans un autre elt du dom',
      textModal:'text send by props',
      showModal : false,
      showModalSlot : false,
      showModalTeleport : false
    }
  },
  methods : {
    toggleModal () {
      console.log()
      this.showModal = !this.showModal
    },
    toggleModalSlot () {
      this.showModalSlot = !this.showModalSlot
    },
    toggleModalTeleport () {
      this.showModalTeleport = !this.showModalTeleport
    }

  }
}
</script>

<style>
#app, .modalsTeleport {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 , {
  border-bottom: 1px solid #ddd;
  display: inline-block;
  padding-bottom: 10px;
}
</style>
