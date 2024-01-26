<template>
  <div id="app">
    <h1>CRUD</h1>

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
      console.log(items, 'salam alyekmom');
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
      let data = item
      let date = new Date()
      let day = date.get()
      data.created_date = day
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
#app {
  font-family: "Helvetica Neue", Arial, sans-serif;
  color: #212b34;
  margin-top: 60px;
  background-color: rgba(0, 0, 0, 0.147);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(30, 28, 31, 0);
}

.form {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 50px;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.form label {
  display: block;
  margin-bottom: 5px;
}

.form input,
.form select {
  padding: 10px;
  border: 2px solid #3498db;
  border-radius: 5px;
  width: 100%;
}

.item-list {
  list-style-type: none;
  padding: 0;
  margin-top: 20px;
}

.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.btn-container button {
  margin-left: 5px;
  padding: 5px 10px;
}

.btn_delete {
  background-color: #f44336;
  color: white;
  border: 2px solid #f44336;
  transition-duration: 0.5s;
  border-radius: 5px;
}

.btn_delete:hover {
  border: 2px solid #f44336;
  color: black;
  background-color: white;
}

.btn_edit {
  background-color: white;
  color: black;
  transition-duration: 0.5s;
  border: 2px solid #e4f806;
  border-radius: 5px;
}

.btn_edit:hover {
  color: black;
  background-color: #e4f806;
}

.btn_add {
  padding: 10px;
  background-color: white;
  color: #04aa6d;
  border: 2px solid #04aa6d;
  border-radius: 5px;
  cursor: pointer;
  transition-duration: 0.5s;
  width: 100%;
  margin-top: 10px;
}

.btn_add:hover {
  color: white;
  background-color: #04aa6d;
  box-shadow: 7px 7px 10px -2px rgba(0, 0, 0, 0.75);
}

.btn_save {
}

.modal {
  display: none;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.7);
}

.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>
