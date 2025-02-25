<template>
  <div class="container-fluid justify-content-center" style="margin-top: 5%; display: inline-flex;">
    <div class="menu">
      <ul>
        <li @click="changeView('list')">Listagem</li>
        <li @click="changeView('backoffice')">Backoffice</li>
        <li>Sair</li>
        </ul>
    </div>
    <div class="main-content">
      <List v-if="currentView==='list'"/>
      <Backoffice v-if="currentView==='backoffice'"/>
    </div>
  </div>
</template>

<script>
  import List from "./views/List.vue"
  import Backoffice from "./views/Backoffice.vue";


export default {
  data() {
    return {
      currentView: "list"
    }
  },
  components: {
    List,
    Backoffice
  },
  methods: {
    changeView(view) {
      this.currentView = view;
    }
  }
}

</script>