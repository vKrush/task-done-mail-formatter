<script setup>
import { defineProps } from "vue";
import ListItem from "./ListItem.vue";
import { ref } from "vue";
import { onMounted } from "vue";
import Clipboard from "clipboard";

defineProps({
  listOfDoneJobs: {
    type: Array,
    required: true,
  },
  fromName: {
    type: String,
    required: true,
  },
  toName: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  updateOfDate: {
    type: String,
    required: true,
  },
});

const textToCopy = ref(null);
const copyButton = ref(null);

onMounted(() => {
  // Initialize clipboard.js with the copy button
  const clipboard = new Clipboard(copyButton.value, {
    text: () => textToCopy.value.innerHTML, // Get the HTML content to be copied
  });

  // Listen for the success event
  clipboard.on("success", () => {
    alert("Text copied to clipboard!");
  });

  // Handle error (if any)
  clipboard.on("error", () => {
    alert("Failed to copy text.");
  });
});
</script>

<template>
  <h1>Email Preview</h1>
  <button ref="copyButton" class="btn btn-secondary">
    Copy Formatted Text
  </button>
  <div ref="textToCopy">
    <p>Hello {{ fromName ? fromName : "[From Name]" }},</p>
    <p>
      Below the Updates of
      {{
        updateOfDate
          ? new Date(updateOfDate).getDate() +
            "/" +
            new Date(updateOfDate).getMonth() +
            "/" +
            new Date(updateOfDate).getFullYear()
          : "[dd/mm/yyyy]"
      }}
    </p>
    <h5>{{ title ? title : "[Title]" }} :-</h5>
    <ul class="ps-5">
      <ListItem v-for="item in listOfDoneJobs" :key="item.id" :item="item" />
    </ul>

    <p>Thank You,</p>
    <p>{{ toName ? toName : "[To Name]" }}</p>
  </div>
</template>
