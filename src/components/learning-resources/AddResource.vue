
<template>

  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>Please check all inputs and make sure you enter at least a few characters into each input field.</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>


  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" ref="description"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="link" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>





<script>
export default {
  data(){
    return{
      inputIsInvalid:false,
    }
  },
  inject : ['addResource'],
  methods:{
    submitData(){
      const enterTitle = this.$refs.title.value;
      const enterDescrition = this.$refs.description.value;
      const enterLink = this.$refs.link.value;


      if (
          enterTitle.trim() === '' ||
          enterDescrition.trim() === '' ||
          enterLink.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      this.addResource(enterTitle , enterDescrition , enterLink);

      this.$refs.title.value ='';
      this.$refs.description.value = '';
      this.$refs.link.value = '';
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }
}
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