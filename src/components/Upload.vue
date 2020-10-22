<template>
  <div id="upload">
    <div class="addSnipp">
      <h2>Add a SNIPPet</h2>
      <p>Try Press enter to Upload a Snippet or use the button!</p>
      
      <input
      type="text" placeholder="title"
      v-model="title"
      >
      <input
      type="text" placeholder="content"
      v-model="content"
      >
      <button class="btn" @click="inputData()">Add Snippet</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Upload',
  data() {
    return {
      title: '',
      content: '',
      myInput: '',
    }
  
  },
  methods: {
    inputData: function(){
      
      let myInput = [this.title, this.content]

      this.$emit('inputData', myInput)
      // console.log('(UPLOAD)EMIT - inputData: ', myInput)

    }
  }
}
</script>

<style>
.addSnipp {
  padding: 1rem 2rem;
  border: 1;
  background-color: lightgrey;
  color: black;
}
.addSnipp > input {
  margin: 0px 20px 0px 0px;
  padding: 5px 10px;

}
</style>