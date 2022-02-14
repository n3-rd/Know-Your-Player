<template>
  <div>
    <q-input
      rounded
      outlined
      v-model="text"
      label="Search Player"
      class="q-pa-md"
      color="brand"
      dark
    />
    />
  </div>
</template>

<script>
export default {
  name: "SearchPage",
  data() {
    return {
      text: "",
    };
  },
};
</script>
