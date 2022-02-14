<template>
  <q-page>
    <q-header class="dark poppins">
      <q-toolbar>
        <q-toolbar-title>Know your player</q-toolbar-title>

        <q-btn flat round dense icon="whatshot" />
      </q-toolbar>
    </q-header>

    <SearchPage />
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import SearchPage from "./SearchPage";

export default defineComponent({
  name: "PageIndex",
  components: { SearchPage },
});
</script>
