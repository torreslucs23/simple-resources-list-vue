<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid input"
    @close="confirmError"
  >
    <template #default>
      <p>Unfortunately, at leats one input value is invalid.</p>
      <p>Please, check all your inputs</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">description</label>
        <textarea
          name="description"
          id="description"
          rows="5"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Url</label>
        <input type="url" id="link" name="link" ref="linkInput" />
      </div>
      <div>
        <base-button>Add rersource</base-button>
      </div>
    </form>
  </base-card>
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
      const enteredtitle = this.$refs.titleInput.value;

      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredtitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.$refs.titleInput.value = '';
      this.$refs.descInput.value = '';
      this.$refs.linkInput.value = '';

      this.addResource(enteredtitle, enteredDescription, enteredUrl);
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
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
