<template>
  <div class="modal" v-if="editingModal">
    <div class="modal-content">
      <span class="close" @click="onClose">&times;</span>
      <h2>Редактирование</h2>

      <form-item
        :data="editingItem"
        @edit="onUpdate"
        submit-button-text="Сохранить"
      />
      <button class="btn_cancel" @click="onClose">Отмена</button>
    </div>
  </div>
</template>

<script>
import FormItem from "./FormItem.vue";

export default {
  components: {
    FormItem,
  },
  props: {
    editingItem: Object,
    editingModal: Boolean,
    onUpdate: Function,
    onClose: Function,
  },
};
</script>

<style scoped>
.modal {
  display: none;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
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

.btn_cancel {
  margin-top: 10px;
  background-color: #ccc;
  padding: 10px;
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  border-radius: 5px;
}
</style>
