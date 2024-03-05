<template>
  <BaseDialog v-if="isInputInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <br />
      <p>
        Please check all inputs and make sure you enter at least a few
        characters into each input field.
      </p>
    </template>
    <template v-slot:actions>
      <BaseButton @click="confirmError">Okay</BaseButton>
    </template>
  </BaseDialog>

  <BaseCard>
    <form action="" @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="inputTitle" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          ref="inputDesc"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="inputLink" />
      </div>
      <div>
        <BaseButton type="submit">Add Resource</BaseButton>
      </div>
    </form>
  </BaseCard>
</template>

<script>
export default {
  data() {
    return {
      isInputInvalid: false,
    };
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      let title = this.$refs.inputTitle.value;
      let desc = this.$refs.inputDesc.value;
      let link = this.$refs.inputLink.value;

      if (!title.trim() || !desc.trim() || !link.trim()) {
        console.log('Inputs are invalid');
        this.isInputInvalid = true;
        return;
      }

      this.addResource(title, desc, link);

      this.$refs.inputTitle.value =
        this.$refs.inputDesc.value =
        this.$refs.inputLink.value =
          '';
    },
    confirmError() {
      this.isInputInvalid = false;
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
