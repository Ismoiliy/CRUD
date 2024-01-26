<template>
  <div class="item-list-container">
  <ul class="item-list">
    <li v-for="item in items" :key="item.id" class="list-item">
      <span>{{ item.name_uz }}</span>
      <div class="btn-container">
        <button class="btn_edit" @click="editItem(item)">Редактировать</button>
        <button class="btn_delete" @click="deleteItem(item.id)">Удалить</button>
      </div>
    </li>
  </ul>
</div>
</template>

<script>
export default {
  props: {
    items: Array,
    onEdit: Function,
    onDelete: Function,
  },
  methods: {
    editItem(item) {
      this.$emit("on-edit", item);
      console.log(item);
    },
    deleteItem(itemId) {
      this.$emit("on-delete", itemId);
    },
  },
};
</script>

<style scoped>
.item-list-container {
  padding: 20px;
  background-color: rgba(82, 100, 118, 0.7);
  border-radius: 10px;
  border: 2px solid #2b2b2b; 
  width: 80%;
  margin: 0 auto;
  margin-top: 20px;
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
  border: 1px solid #3498db;
  border-radius: 5px;
  color: #fff; 
}

.btn-container button {
  margin-left: 5px;
  padding: 5px 10px;
}

.btn_delete {
  background-color: #fff;
  color: #2b2b2b;
  border: 2px solid #f44336;
  transition-duration: 0.5s;
  border-radius: 5px;
}

.btn_delete:hover {
  border: 2px solid #f44336;
  color: #fff; 
  background-color: #f44336;
  box-shadow: 7px 7px 10px -2px rgba(0, 0, 0, 0.75);
}

.btn_edit {
  background-color: #fff; 
  color: #2b2b2b;
  transition-duration: 0.5s;
  border: 2px solid #e4f806;
  border-radius: 5px;
}

.btn_edit:hover {
  color: #2b2b2b;
  background-color: #e4f806;
  box-shadow: 7px 7px 10px -2px rgba(0, 0, 0, 0.75);
}
</style>
