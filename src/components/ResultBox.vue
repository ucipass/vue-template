<template>
  <b-container fluid>
    <b-row >Result</b-row>
    <b-row >
        <b-form-textarea
        :value="message"
        placeholder="Auto height textarea"
        rows="5"
        max-rows="20"
        ></b-form-textarea>
    </b-row> 
  </b-container>
 
</template>

<script>
export default {
  name: 'ResultBox',
  props: {
    message: {
      default: "Empty",
      type: String
    }
  },
  mounted: function () {
    // this.$nextTick(() => {
    //   this.$bvModal.show('modal-1')
    // })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
