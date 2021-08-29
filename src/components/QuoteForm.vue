<template>
  <div class="quoteForm">
    <div class="form-group">
      <label>Quote:</label>
      <input type="text" class="form-control" v-model="quoteData.Quote" />
    </div>
    <div class="form-group">
      <label>Author:</label>
      <input type="text" class="form-control" v-model="quoteData.Author" maxlength="50" />
    </div>
    <div class="form-group">
      <label>Source:</label>
      <input type="text" class="form-control" v-model="quoteData.Source" maxlength="100" />
    </div>
  </div>
</template>

<script>
export default {
  name: "quoteForm",
  props: {
    quoteData: Object
  }
}
</script>

<style scoped>

.form-control {
  width: 50vw;
  height: 25px;
  margin-top: 10px;
}

label {
  margin-right: 7px;
}

.quoteForm {
  margin-top: 30px;
}
</style>