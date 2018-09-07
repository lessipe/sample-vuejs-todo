<template>
  <button
    type="button"
    class="list-group-item list-group-item-action"
    :class="buttonStyle"
    @click="$emit('toggleStatus')"
  >
    {{ title }}
  </button>
</template>
<script>
  export default {
    props: ['title', 'status'],
    computed: {
      buttonStyle() {
        if (this.status === 'done') {
          return ['list-group-item-success'];
        }

        return [];
      }
    }
  };
</script>
