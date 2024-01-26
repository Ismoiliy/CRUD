<template>
  <div id="app">
    <nav class="navbar">
      <div class="container-fluid">
        <span class="navbar-title">СRUD</span>
      </div>
    </nav>
    <div class="main">
      <form-item
        v-if="editingItem"
        :data="editingItem"
        @edit="updateItem"
        submit-button-text="Сохранить"
      />
      <form-item
        v-else
        :item="newItem"
        @submit="createItem"
        submit-button-text="Добавить"
      />

      <item-list
        :items="items"
        @on-edit="openEditModal"
        @on-delete="deleteItem"
      />

      <edit-modal
        :editing-item="editingItem"
        :editing-modal="editingModal"
        @on-update="saveEdit"
        @on-close="closeEditModal"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import FormItem from "./components/FormItem.vue";
import ItemList from "./components/ItemList.vue";
import EditModal from "./components/EditModal.vue";

export default {
  components: {
    FormItem,
    ItemList,
    EditModal,
  },
  data() {
    return {
      items: [],
      newItem: {
        product_type_id: null,
        name_uz: "",
        cost: null,
        address: "",
        created_date: null,
      },
      editingItem: null,
      editingModal: false,
    };
  },
  mounted() {
    this.getItems();
  },
  methods: {
    getItems() {
      axios
        .get("http://94.158.54.194:9092/api/product")
        .then((response) => {
          this.items = response.data;
        })
        .catch((error) => {
          console.error("Ошибка при получении данных:", error);
        });
    },
    createItem(items) {
      console.log(items, "salam aleykom");
      axios
        .post("http://94.158.54.194:9092/api/product", items)
        .then(() => {
          this.newItem = {
            product_type_id: "",
            name_uz: "",
            cost: null,
            address: "",
            created_date: null,
          };
          this.getItems();
        })
        .catch((error) => {
          console.error("Ошибка при создании элемента:", error);
        });
    },
    updateItem(item) {
      let data = item;
      let date = new Date();
      let day = date.getDate();
      data.created_date = day;
      axios
        .put(`http://94.158.54.194:9092/api/product/`, data)
        .then(() => {
          this.editingItem = null;
          this.getItems();
        })
        .catch((error) => {
          console.error("Ошибка при редактировании элемента:", error);
        });
    },
    deleteItem(itemId) {
      axios
        .delete(`http://94.158.54.194:9092/api/product/${itemId}`)
        .then(() => {
          this.getItems();
        })
        .catch((error) => {
          console.error("Ошибка при удалении элемента:", error);
        });
    },
    openEditModal(item) {
      console.log(item);
      this.editingItem = { ...item };
      this.editingModal = true;
    },
    closeEditModal() {
      this.editingModal = false;
    },
    saveEdit(item) {
      this.updateItem(item);
      this.closeEditModal();
    },
  },
};
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

#app {
  font-family: "Helvetica Neue", Arial, sans-serif;
  color: #fff; 
  background-color: #2b2b2b; 
  height: 100%;
}

.navbar-title {
  color: #A7B2B8;
  display: flex;
  align-items: center;
  justify-content: center;
}

.navbar {
  font-size: 40px;
  margin-bottom: 50px;
  margin-left: 10px;
}

</style>

