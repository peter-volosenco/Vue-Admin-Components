<template>
  <div>
    <table v-if="selectedItem == null" border="1">
      <tr>
        <td>ID</td>
        <td>Name</td>
        <td>Text</td>
        <td>Order</td>
        <td>Actions</td>
      </tr>
      <tr v-for="(item, index) in vItems" :key="item.Id">
        <td>{{ item.Id }}</td>
        <td>{{ item.Name }}</td>
        <td>{{ item.Text }}</td>
        <td>{{ item.Order }}</td>
        <td @click="editItem(item, index)">Edit</td>
      </tr>
    </table>

    <AdminView
      v-if="selectedItem != null"
      :item="selectedItem"
      :index="selectedIndex"
      v-on:save="save"
      v-on:back="clearSelection"
    ></AdminView>
  </div>
</template>

<script>
import AdminView from './AdminView.vue';

export default {
  name: 'AdminGrid',
  props: {
    items: {
      type: Array,
    },
  },
  components: {
    AdminView,
  },
  data: function () {
    return {
      selectedItem: null,
      selectedIndex: null,
      vItems: [],
    };
  },
  watch: {
    //once data restored from local storage, update
    items: function (newVal) {
      this.vItems = newVal;
    },
  },
  methods: {
    clearSelection() {
      this.selectedItem = null;
      this.selectedIndex = null;
    },
    editItem(item, index) {
      this.selectedItem = item;
      this.selectedIndex = index;
    },
    updateItem(item, index) {
      this.vItems[index] = item;
    },
    save(item, index) {
      this.updateItem(item, index);
      this.$emit('newList', this.vItems);
      this.clearSelection();
    },
  },
  mounted() {
    //initial load, update
    this.vItems = this.items;
  },
};
</script>

<style>
table {
  text-align: center;
  max-width: 680px;
  margin: 0 auto;
}

tr:first-child {
  font-weight: bold;
}
</style>
