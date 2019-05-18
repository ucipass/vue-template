<template>
  <div>
    <h1>{{ msg }}</h1>
    <b-modal id="modal-1" class="text-center" title="Login">
        <b-container>
          <b-row class="my-1">
            <b-col sm="3">
              <label>Username</label>
            </b-col>
            <b-col sm="9">
              <b-form-input id='username' type="text" v-model='username'></b-form-input>
            </b-col>
          </b-row>
          <b-row class="my-1">
            <b-col sm="3">
              <label>Password</label>
            </b-col>
            <b-col sm="9">
              <b-form-input id='password' type="password" v-model="password"></b-form-input>
            </b-col>
          </b-row>                
        </b-container>
        <div slot="modal-footer" class="w-100">
          <p class="float-left"></p>
          <b-button variant="primary" size="sm" class="float-right" @click="hidemod">Login</b-button>
        </div>
    </b-modal>
  </div>
</template>

<script>

export default {
  name: 'Modal',
  props: {
    msg: String
  },
  data: function(){
    return{
      username: 'myuser',
      password: 'mypass'
    }
  },
  methods:{
    showmod: function(){
      this.$bvModal.show('modal-1')
    },
    hidemod: function(){
      this.$bvModal.hide('modal-1')
    },
    login: function(){
      // eslint-disable-next-line 
      console.log('username',this.username,'password',this.password)
    }
  },
  mounted: function () {
    this.$nextTick(() => {
      this.$bvModal.show('modal-1')
    })
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
