<template>
  <teleport to="body">
  <div v-if="visible" class="dialog">
    <div class="dialog-content">
      <h3>{{ title }}</h3>
      <div class="dialog-body">
        <slot></slot>
      </div>
      <div class="dialog-actions">
        <slot name="action"></slot>
      </div>
    </div>
  </div>
  </teleport>
</template>


<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    visible: {
      type: Boolean,
      default: true
    }
  }
};
</script>


<style scoped>
.dialog {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  padding: 1rem;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
.dialog-content {
  padding: 1rem;
}
.dialog-body {
  margin-bottom: 1rem;
}
.dialog-actions {
  text-align: right;
}
</style>
