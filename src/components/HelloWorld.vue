<template>
  <div>
    <h1>{{ msg }}</h1>
    <item-list />
  </div>
</template>

<script>
import ItemList from "./ItemList.vue";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    ItemList,
  },
};
</script>
