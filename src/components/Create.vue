<script lang="ts" setup>
import { reactive, defineProps, onMounted, PropType, ref, watch } from "vue";
import type { Item } from "../models/item";

const show = defineModel({
  default: false,
  required: true,
  type: true,
});

const props = defineProps({
  items: {
    type: Array as PropType<Item[]>,
    required: true,
  },
});

const emits = defineEmits<{
  create: [value: Item];
}>();

const item = reactive<Item>({
  id: null,
  name: null,
  description: null,
});

const isValid = ref<boolean>(false);

const onSubmit = () => {
  emits("create", { ...item, id: props.items.length + 1 });
  show.value = false;
};
</script>

<template>
  <v-dialog v-model="show" width="500px">
    <v-card>
      <v-card-text>
        <v-form v-model="isValid" @submit.prevent="onSubmit">
          <v-text-field
            v-model="item.name"
            label="Name"
            :rules="[(v:string) => !!v || 'Name is required']"
          />
          <v-textarea v-model="item.description" />
          <v-btn type="submit">Add</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>
