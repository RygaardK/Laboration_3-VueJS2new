<template>
  <div id="latestsnipps">
    <div class="listSnippet">
      <h3>Our Snippets!</h3>
      <ol>
        <li v-for="snipp in passthru" :key="snipp.id">
          <p class="snippDelete" @click="deleteSnipp(snipp.id)">Delete</p>
          <p class="snippID">{{ snipp.id }}</p>
          <p class="snippLable1">Title:</p>
          <p class="snippValue1">{{ snipp.title }}</p>  
          <p class="snippLable2">Content:</p>
          <p class="snippValue2">{{ snipp.content }}</p> 
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Latestsnipps',
  props: {
    passthru: Array
  },
  methods: {
    deleteSnipp: function(id){
      this.$emit('deleteSnippet', id)
      console.log('(LATEST)EMIT - deleteSnipp: ', id)

    }
  }
}
</script>

<style>
#latestsnipps{
  width: 100vw;
}
.listSnippet {
  padding: 2rem;
}
.listSnippet p {
  display: inline;
}
.snippID,.snippLable1, .snippValue1, .snippLable2, .snippValue2 {
  padding: 10px 10px 0px 0px;
}

.listSnippet ol {
  list-style-type: upper-roman;
}
.listSnippet ol li {
  padding: 0px 10px 10px 0px;
}
.snippDelete {
  padding: 3px;
  border-radius: 5px;
  color: white;
  background-color: red;
  text-align: justify;

}
.snippLable1, .snippLable2 {
  font-weight: bold;
}

</style>