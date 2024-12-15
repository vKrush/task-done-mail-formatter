<script setup>
import { defineEmits, defineModel } from "vue";

defineProps({
  index: {
    type: Number,
    required: true,
  },
});

defineModel("item", {
  type: Object,
  required: true,
});

const emit = defineEmits(["addNewChild", "addNewChildItem", "removeItem"]);

const onAddNewChildItem = (item) => {
  emit("addNewChildItem", item);
};

const onRemoveItem = (id) => {
  console.log(id);
  emit("removeItem", id);
};
</script>

<template>
  <div class="row mt-3">
    <div class="col-3">
      <button class="btn btn-dark w-100" @click="onAddNewChildItem(item)">
        Add Child
      </button>
    </div>
    <div class="col-8">
      <input
        type="text"
        class="form-control"
        id="title-name"
        placeholder="Enter title name"
        v-model="item.name"
      />
    </div>
    <div class="col-1">
      <button class="btn" @click="onRemoveItem(item.id)">🗑️</button>
    </div>
    <div class="col mt-3 px-5">
      <InputControl
        v-for="(child, cIndex) in item.children"
        :key="child.id"
        :item="child"
        :index="cIndex"
        @add-new-child-item="onAddNewChildItem"
        @remove-item="onRemoveItem"
      />
    </div>
  </div>
</template>
