<template>
  <Toast 
    v-if="toastShow"
    :message="toastMessage"
    :isError="toastError"
    @closeToast="closeToast"
  />

  <div class="container-fluid justify-content-center" style="margin-top: 5%; display: inline-flex;">
    <div class="menu">
      <ul>
        <li @click="changeView('list')">Listagem</li>
        <li @click="changeView('backoffice')">Backoffice</li>
        <li>Sair</li>
        </ul>
    </div>
    <div class="main-content">
      <List v-if="currentView==='list'" :showToast="showToast"/>
      <Backoffice v-if="currentView==='backoffice'"/>
    </div>
  </div>
</template>

<script>
  import List from "./views/List.vue"
  import Backoffice from "./views/Backoffice.vue";
  import Toast from "./components/Toast.vue";

export default {
  data() {
    return {
      currentView: "list",
      
      toastShow: false,
      toastError: true,
      toastMessage: ""
    }
  },
  components: {
    List,
    Backoffice,
    Toast
  },
  methods: {
    changeView(view) {
      this.currentView = view;
    },
    showToast(message, isError) {
      this.toastMessage = message;
      this.toastShow = true;
      this.toastError = isError;
    },
    closeToast() {
      this.toastShow = false;
    }
  }
}

</script>