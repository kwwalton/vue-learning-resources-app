<template>
<base-dialog v-if="inputIsInvalid" @close="confirmError" title="Invalid Input">
  <template #default><p>Unfortunately at least one input is invalid.</p></template>
  <template #actions>
    <base-button @click="confirmError">Okay</base-button>
  </template>
</base-dialog>
  <base-card>
    <form @submit.prevent="submitAction">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" v-model="resourceTitle" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          v-model="resourceDescription"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" v-model="resourceLink" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  name: 'AddResource',
  data() {
    return {
      resourceTitle: '',
      resourceDescription: '',
      resourceLink: '',
      resourceTitleError: false,
      resourceDescriptionError: false,
      resourceLinkError: false,
      inputIsInvalid: false,
    };
  },
  inject: ['addResource'],
  methods: {
    resetForm() {
      this.resourceTitle = ''
      this.resourceDescription = ''
      this.resourceLink = ''
    },

    confirmError() {
      this.inputIsInvalid = false
    },

    submitAction() {
      // validate first
      const title = this.resourceTitle.trim();
      const description = this.resourceDescription.trim();
      const link = this.resourceLink.trim();

      if (title.length > 0 && description.length > 0 && link.length > 0) {
        const newResource = {
          id: new Date().toISOString(),
          title,
          description,
          link,
        };
        // use provide and inject instead of emit
        this.addResource(newResource);
        // reset values
        this.resetForm()
      } else {
        this.inputIsInvalid = true
        //alert('not all fields valid')
      }
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