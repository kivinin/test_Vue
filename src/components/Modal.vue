<template>
    <div class="modal">
      <div class="groupTitle">
        <div>Добавление пользователя</div>
        <div @click="closeModal" class="closeModal"></div>
      </div>
      <div class="groupTableName">
        <label>Имя</label>
        <input v-model="form.name" type="text" />
      </div>
      <div class="groupTableName">
        <label>Телефон</label>
        <input v-model="form.age" type="tel" placeholder="+7" />
      </div>
      <div class="groupTableName">
        <label>Начальник</label>
        <select v-model="form.parent">
          <option v-for="item in items" :value="item.id" :key="item.id">
            {{ item.name }}
          </option>
        </select>
      </div>
      <button @click="saveItem">Сохранить</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      items: {
        type: Array,
        default: () => [],
      },
    },
    data() {
      return {
        form: {
          name: "",
          age: "",
          parent: null,
        },
      };
    },
    methods: {
      saveItem() {
        const newItem = {
          id: Date.now(),
          name: this.form.name,
          age: this.form.age,
          parent: this.form.parent,
        };
        this.$emit("save-item", newItem);
      },
      closeModal() {
        this.$emit("close-modal");
      },
    },
  };
  </script>
  
  <style>
  .modal {
    border: 1px solid #ccc;
    padding: 20px;
    background-color: #fff;
    position: fixed;
    top: 50%;
    left: 50%;
    width: 300px;
    transform: translate(-50%, -50%);
  }
  .groupTableName {
    display: flex;
    justify-content: space-between;
  }
  .groupTitle {
    display: flex;
    justify-content: space-between;
    margin: 10px;
  }
  .closeModal {
    width: 24px;
    height: 24px;
    opacity: 0.2;
    cursor: pointer;
    transition: opacity ease 0.5s;
  }
  .closeModal:hover {
    opacity: 1;
  }
  .closeModal::before,
  .closeModal::after {
    content: "";
    position: absolute;
    display: block;
    width: 24px;
    height: 3px;
    background: #000;
  }
  .closeModal::before {
    transform: rotate(45deg);
  }
  .closeModal::after {
    transform: rotate(-45deg);
  }
  </style>
  