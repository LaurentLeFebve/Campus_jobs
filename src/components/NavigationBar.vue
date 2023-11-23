<template>
  <v-app-bar color="teal-darken-4">
    <template v-slot:image>
      <v-img
        gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
      ></v-img>
    </template>

    <v-app-bar-title>Campus Jobs</v-app-bar-title>

    <v-spacer></v-spacer>

    <v-btn icon @click="isSearching = !isSearching">
      <v-icon>mdi-magnify</v-icon>
    </v-btn>
    <v-text-field
      v-if="isSearching"
      v-model="searchWord"
      label="Suche"
      autofocus
    ></v-text-field>

    <v-menu>
      <template v-slot:activator="{ props }">
        <v-btn icon v-bind="props"> <v-icon>mdi-dots-vertical</v-icon></v-btn>
      </template>
      <v-list>
        <v-list-item value="Mein Konto">
          <v-list-item-title
            ><v-icon>mdi-account</v-icon> Konto</v-list-item-title
          >
        </v-list-item>
        <v-list-item value="Einstellungen">
          <v-list-item-title
            ><v-icon>mdi-nut</v-icon> Einstellungen</v-list-item-title
          >
        </v-list-item>
        <v-list-item value="Benachrichtigungen">
          <v-list-item-title
            ><v-icon>mdi-bell</v-icon> Benachrichtigungen</v-list-item-title
          >
        </v-list-item>
      </v-list>
    </v-menu>
  </v-app-bar>
</template>

<script setup>
import { ref, computed, defineEmits, watch } from "vue";

const emit = defineEmits();

let items = ["Konto", "mdi-clock"];

let searchWord = ref("");

let isSearching = ref(false);

watch(searchWord, (newVal, oldVal) => {
  emit("search", newVal);
});
</script>
