<script setup>
import InputControl from "./InputControl.vue";

const listId = defineModel("listId", {
  type: Number,
  required: true,
});
const listOfDoneJobs = defineModel("listOfDoneJobs", {
  type: Array,
  required: true,
});

const fromName = defineModel("fromName", {
  type: String,
  required: true,
});

const toName = defineModel("toName", {
  type: String,
  required: true,
});

const title = defineModel("title", {
  type: String,
  required: true,
});

const updateOfDate = defineModel("updateOfDate");

const addNewItem = () => {
  listOfDoneJobs.value.push({
    id: listId.value++,
    name: "",
    children: [],
  });
};

const addNewChildItem = (item) => {
  item.children.push({
    id: listId.value++,
    name: "",
    children: [],
  });
};

const removeItem = (rId) => {
  console.log(rId);
  listOfDoneJobs.value = removeI(listOfDoneJobs.value, rId);
};

const removeI = (list, rId) => {
  console.log(list);
  return list.filter((item) => {
    if (item.id != rId) {
      if (item.children.length > 0) {
        console.log(item.children);
        item.children = removeI(item.children, rId);
      }
      return item;
    }
  });
};
</script>

<template>
  <h1>Email Form</h1>
  <div class="container">
    <div class="row">
      <div class="col-6">
        <div class="mb-3">
          <label for="from-name" class="form-label"> From Name </label>
          <input
            type="text"
            class="form-control"
            id="from-name"
            placeholder="Enter from name"
            v-model="fromName"
          />
        </div>
      </div>
      <div class="col-6">
        <div class="mb-3">
          <label for="to-name" class="form-label"> To Name </label>
          <input
            type="text"
            class="form-control"
            id="to-name"
            placeholder="Enter to name"
            v-model="toName"
          />
        </div>
      </div>
      <div class="col-6">
        <div class="mb-3">
          <label for="title-name" class="form-label"> Title Name </label>
          <input
            type="text"
            class="form-control"
            id="title-name"
            placeholder="Enter title name"
            v-model="title"
          />
        </div>
      </div>
      <div class="col-6">
        <div class="mb-3">
          <label for="update-date" class="form-label"> Updates Of Date </label>
          <input
            type="date"
            class="form-control"
            id="update-date"
            placeholder="Enter Date"
            v-model="updateOfDate"
          />
        </div>
      </div>

      <div class="col-12">
        <div class="mb-3">
          <div class="container">
            <div class="row mb-3">
              <div class="col d-flex align-items-center">
                <label for="title-name" class="form-label">
                  List Of Done Jobs
                </label>
              </div>
              <div class="col d-flex justify-content-end">
                <button class="btn btn-dark w-25" @click="addNewItem">
                  Add
                </button>
              </div>
            </div>
            <!-- <div
              class="row mb-3"
              v-for="(item, index) in listOfDoneJobs"
              :key="item.id"
            >
              <div class="col-2">
                <button class="btn btn-dark w-100" @click="addNewChild(index)">
                  Add Child
                </button>
              </div>
              <div class="col-9">
                <input
                  type="text"
                  class="form-control"
                  id="title-name"
                  placeholder="Enter title name"
                  v-model="item.name"
                />
              </div>
            </div> -->
            <InputControl
              v-for="(item, index) in listOfDoneJobs"
              :key="item.id"
              :item="item"
              :index="index"
              @add-new-child-item="addNewChildItem"
              @remove-item="removeItem"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
