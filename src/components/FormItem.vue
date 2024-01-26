<template>
  <form class="form" @submit.prevent="submitForm">
    <div v-if="!data1">
      <div class="form-container">
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
    </div>
    <div v-else>
      <div class="form-container">
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
    </div>
    <button class="btn_add" type="submit">{{ submitButtonText }}</button>
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
      console.log("Edit button clicked");
      if (this.data1) {
        this.$emit("edit", this.data1);
      }
      this.$emit("submit", this.item);
    },
  },
  watch: {
    data: {
      handler(newValue) {
        console.log(newValue);
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

<style>
.form {
  padding: 20px;
  border: 2px solid #2b2b2b;
  box-shadow: 0px 0px 66px -9px rgba(0, 0, 0, 0.38);
  border-radius: 10px;
  background-color: rgba(82, 100, 118, 0.7);
  width: 60%;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 15px;
  width: 16%;
}
.form-container {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  margin-left: -20px;
  gap: 20px;
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

.btn_add {
  padding: 15px;
  background-color: #fff;
  color: #04aa6d; 
  border: 2px solid #04aa6d;
  border-radius: 5px;
  cursor: pointer;
  transition-duration: 0.5s;
  margin-top: 10px;
  margin-left: 15px;
}
.btn_add:hover {
  color: #2b2b2b; 
  background-color: #04aa6d;
  box-shadow: 7px 7px 10px -2px rgba(0, 0, 0, 0.75);
}
</style>

