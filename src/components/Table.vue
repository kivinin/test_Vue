<template>
    <div class="groupTable">
      <table>
        <thead>
          <tr>
            <th @click="sortBy('name')">Имя</th>
            <th @click="sortBy('age')">Телефон</th>
            <th @click="sortBy('parent')">Начальник</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in sortedItems" :key="item.id">
            <td>{{ item.name }}</td>
            <td>{{ item.age }}</td>
            <td>{{ getParentName(item.parent) }}</td>
          </tr>
        </tbody>
      </table>
      <button @click="openModal">Добавить</button>
      <Modal
        v-if="showModal"
        @close-modal="closeModal"
        @save-item="saveItem"
        :items="items"
      ></Modal>
    </div>
  </template>
  
  <script>
  import Modal from "./Modal.vue";
  
  export default {
    components: {
      Modal,
    },
    data() {
      return {
        items: [],
        showModal: false,
        form: {
          name: "",
          age: "",
          parent: null,
        },
        sortColumn: null,
        sortDirection: 1,
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      fetchData() {
        const savedData = localStorage.getItem("tableData");
        if (savedData) {
          this.items = JSON.parse(savedData);
        }
      },
      saveData() {
        const data = JSON.stringify(this.items);
        localStorage.setItem("tableData", data);
      },
      openModal() {
        this.showModal = true;
      },
      closeModal() {
        this.showModal = false;
        this.resetForm();
      },
      saveItem(newItem) {
        this.items.push(newItem);
        this.saveData();
        this.resetForm();
      },
      resetForm() {
        this.form.name = "";
        this.form.age = "";
        this.form.parent = null;
      },
      getParentName(parentId) {
        const parent = this.items.find((item) => item.id === parentId);
        return parent ? parent.name : "-";
      },
      sortBy(column) {
        if (this.sortColumn === column) {
          this.sortDirection *= -1;
        } else {
          this.sortColumn = column;
          this.sortDirection = 1;
        }
        this.items.sort((a, b) => {
          const valueA = a[column];
          const valueB = b[column];
          if (valueA < valueB) return -1 * this.sortDirection;
          if (valueA > valueB) return 1 * this.sortDirection;
          return 0;
        });
      },
    },
    computed: {
      sortedItems() {
        return this.items;
      },
    },
  };
  </script>
  
  <style>
  .groupTable {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  table {
    border-collapse: collapse;
  }
  th,
  td {
    border: 1px solid black;
  }
  </style>
  