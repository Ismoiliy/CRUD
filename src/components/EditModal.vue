<template>
  <div class="modal">
    <div class="modal-content">
      <span class="close" @click="onClose">&times;</span>
      <h2>Редактирование</h2>

      <form-item
        :item="editingItem"
        :on-submit="onUpdate"
        submit-button-text="Сохранить"
      />
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
