<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import EmailForm from "./components/EmailForm.vue";
import EmailPreview from "./components/EmailPreview.vue";

import { ref } from "vue";
const listId = ref(0);
const listOfDoneJobs = ref([]);
const fromName = ref("");
const toName = ref("");
const title = ref("");
const today = new Date();
const updateOfDate = ref(
  `${today.getFullYear()}-${today.getMonth()}-${today.getDate()}`
);
</script>

<template>
  <div class="container-fluid" style="min-height: 100vh">
    <div class="row">
      <div class="col-6 border" style="min-height: 100vh">
        <EmailForm
          v-model:list-id="listId"
          v-model:list-of-done-jobs="listOfDoneJobs"
          v-model:from-name="fromName"
          v-model:to-name="toName"
          v-model:title="title"
          v-model:update-of-date="updateOfDate"
        />
      </div>
      <div class="col-6 border" style="min-height: 100vh">
        <EmailPreview
          :list-of-done-jobs="listOfDoneJobs"
          :from-name="fromName"
          :to-name="toName"
          :title="title"
          :update-of-date="updateOfDate"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
