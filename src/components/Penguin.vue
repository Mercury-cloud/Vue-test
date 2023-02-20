<template>
  <li>
    <!-- Display the penguin's name and rating. -->
    <span>{{ name }}</span
    >: <span>{{ rating }}</span>
    <!-- The penguin is being passed as a prop -->
  </li>
</template>

<script>
export default {
  props: {
    penguin: {
      type: Object,
      default: () => ({}),
    },
  },
  computed: {},
  data() {
    return {
      name: this.penguin.name,
      rating: this.penguin.rating,
    };
  },
};
</script>
