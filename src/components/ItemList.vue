<template>
  <ul class="item-list">
    <li v-for="item in items" :key="item.id" class="list-item">
      <span>{{ item.name_uz }}</span>
      <div class="btn-container">
        <button class="btn_edit" @click="editItem(item)">Редактировать</button>
        <button class="btn_delete" @click="deleteItem(item.id)">Удалить</button>
      </div>
    </li>
  </ul>
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
</style>
