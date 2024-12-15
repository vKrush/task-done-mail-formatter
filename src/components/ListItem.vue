<script setup>
defineProps({
  item: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <li>
    <h6>{{ item.name }}</h6>
    <ul v-if="item.children.length">
      <ListItem v-for="child in item.children" :key="child.id" :item="child" />
      <!-- <li v-for="child in item.children" :key="child.id">{{ child.name }}</li> -->
    </ul>
  </li>
</template>
