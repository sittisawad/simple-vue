<script lang="ts" setup>
import { ref } from "vue";
import { Item } from "../models/item";
import Create from "./Create.vue";

const showDialog = ref<boolean>(false);
const items = ref<Item[]>([{ id: 1, name: "TEST", description: "Test" }]);

const onCreateItem = (item: Item) => {
  items.value.push(item);
};
</script>
<template>
  <v-container>
    <v-row>
      <v-col>
        <v-btn density="comfortable" @click="showDialog = true">Add</v-btn>
      </v-col>
      <v-col cols="12">
        <v-data-table :items="items"> </v-data-table>
      </v-col>
    </v-row>
  </v-container>
  <Create v-model="showDialog" :items="items" @create="onCreateItem" />
</template>
<style>
.v-table {
  width: 600px;
}
</style>
