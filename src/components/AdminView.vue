<template>
  <div class="wrap">
    <div class="navigation" @click="$emit('back')">&#60; Back</div>
    <div class="item">
      <label>Id</label>
      <input type="text" disabled v-model="newItem.Id" />
    </div>
    <div class="item">
      <label>Name</label>
      <input type="text" v-model="newItem.Name" />
    </div>
    <div class="item">
      <label>Text</label>
      <textarea :value="item.Text" rows="5" v-model="newItem.Text" />
    </div>
    <div class="item">
      <label>Order</label>
      <input type="text" :value="item.Order" v-model="newItem.Order" />
    </div>
    <div class="save" @click="$emit('save', newItem, index)">Save</div>
  </div>
</template>

<script>
export default {
  name: 'AdminView',
  props: {
    index: {
      type: Number,
    },
    item: {
      type: Object,
    },
  },
  data: function () {
    return {
      newItem: {},
    };
  },
  mounted() {
    this.newItem = this.item;
  },
};
</script>

<style lang="scss" scoped></style>
