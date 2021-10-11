<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input">
    <!-- Another way to access slot -->
    <template #default>
      <p>Please enter values in all input fields!!!!</p>
    </template>
    <template v-slot:actions>
      <base-button @click="closeDialog">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <input
          id="title"
          type="text"
          placeholder="Please enter a title"
          ref="titleInput"
        />
      </div>

      <div class="form-control">
        <input
          id="description"
          type="text"
          placeholder="Please enter description"
          rows="3"
          ref="descriptionInput"
        />
      </div>
      <div class="form-control">
        <input
          id="link"
          type="url"
          placeholder="Please enter link"
          ref="linkInput"
        />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descriptionInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
    closeDialog() {
      this.inputIsInvalid = false;
    }
  }
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
