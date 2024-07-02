<template>
    <div>
      <base-dialog v-if="inputIsInvalid" title="Invalid INPUT">
        <template #default>
          <p>Unfortunately, at least one input value is invalid.</p> 
          <p>Please check all inputs.</p>
        </template>
        <template #action>
          <base-button @click="confirmError">OK</base-button>
        </template>
      </base-dialog>
  
      <base-card>
        <form @submit.prevent="submitData">
          <div class="form-control">
            <label for="title">Title</label>
            <input id="title" name="title" type="text" ref="titleInput" />
          </div> 
          <div class="form-control">
            <label for="description">Description</label>
            <textarea id="description" name="description" rows="3" ref="descInput"></textarea>
          </div> 
          <div class="form-control">
            <label for="link">Link</label>
            <input id="link" name="link" type="url" ref="linkInput" />
          </div>
          <div>
            <base-button type="submit">Add Resource</base-button>
          </div>
        </form>
      </base-card>
    </div>
  </template>
  

  <script>
  export default {
    inject: ['addResource'],
    data() {
      return {
        inputIsInvalid: false,
      };
    },
    methods: {
      submitData() {
        const enteredTitle = this.$refs.titleInput.value.trim();
        const enteredDescription = this.$refs.descInput.value.trim();
        const enteredUrl = this.$refs.linkInput.value.trim();
  
        if (enteredTitle.length === 0 || enteredDescription.length === 0 || enteredUrl.length === 0) {
          this.inputIsInvalid = true;
          return;
        }
        this.addResource(enteredTitle, enteredDescription, enteredUrl);
      },
      confirmError() {
        this.inputIsInvalid = false;
      }
    }
  };
  </script>
  



<style scoped>
label {
  display: block;
  font-weight: bold;
  margin-bottom: 0.5rem;
}
input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.20rem;
  border: 1px solid #ccc;
}
input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}
.form-control {
  margin-bottom: 1rem;
}
</style>

