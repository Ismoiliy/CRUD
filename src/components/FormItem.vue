<template>
  <form class="form" @submit.prevent="submitForm">
    <div v-if="!data">
      <div class="form-group">
        <label for="edit_product_type_id">ID Типа продукта:</label>
        <input
          v-model="item.product_type_id"
          type="number"
          id="edit_product_type_id"
        />
      </div>
      <div class="form-group">
        <label for="name_uz">Название:</label>
        <input v-model="item.name_uz" type="text" id="name_uz" required />
      </div>
      <div class="form-group">
        <label for="cost">Стоимость:</label>
        <input v-model="item.cost" type="number" id="cost" required />
      </div>
      <div class="form-group">
        <label for="address">Адрес:</label>
        <input v-model="item.address" type="text" id="address" required />
      </div>
      <div class="form-group">
        <label for="created_date">Created Date:</label>
        <input
          v-model="item.created_date"
          type="date"
          id="created_date"
          required
        />
      </div>
    </div>
    <div v-else>
      <div class="form-group">
        <label for="edit_product_type_id">ID Типа продукта:</label>
        <input
          v-model="data1.product_type_id"
          type="number"
          id="edit_product_type_id"
        />
      </div>

      <div class="form-group">
        <label for="name_uz">Название:</label>
        <input v-model="data1.name_uz" type="text" id="name_uz" required />
      </div>
      <div class="form-group">
        <label for="cost">Стоимость:</label>
        <input v-model="data1.cost" type="number" id="cost" required />
      </div>
      <div class="form-group">
        <label for="address">Адрес:</label>
        <input v-model="data1.address" type="text" id="address" required />
      </div>
    </div>
    <button class="btn_save" type="submit">{{ submitButtonText }}</button>
  </form>
</template>

<script>
export default {
  props: {
    data: Object,
    onSubmitAction: Function,
    submitButtonText: String,
  },
  data() {
    return {
      data1: {},
      item: {
        product_type_id: null,
        name_uz: "",
        cost: null,
        address: "",
        created_date: null,
      },
      localItem: { ...this.item },
    };
  },
  methods: {
    submitForm() {
      console.log(this.item);
      if (this.data1) {
        this.$emit("edit", this.data1);
      }
      this.$emit("submit", this.item);
    },
  },
  watch: {
    data: {
      handler(newValue) {
        this.data1 = newValue;
      },
      deep: true,
      immediate: true,
    },
  },
  mounted() {
    console.log(this.data1);
  },
};
</script>

<style scoped>
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
</style>
