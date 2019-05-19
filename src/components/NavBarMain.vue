<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="#">Home</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item-dropdown text="Menu" right>
            <b-dropdown-item href="#">Menu1</b-dropdown-item>
            <b-dropdown-item href="#">Menu2</b-dropdown-item>
            <b-dropdown-item href="#">Menu3</b-dropdown-item>
            <b-dropdown-item href="#">Menu4</b-dropdown-item>
          </b-nav-item-dropdown>
          <b-form-checkbox v-model="checkedcsv" name="check-button" switch class='text-light m-2'>
            CSV</b>
          </b-form-checkbox>
          <b-form-checkbox v-model="checkedtmp" name="check-button" switch class='text-light m-2'>
            Template</b>
          </b-form-checkbox>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template slot="button-content"><em>User</em></template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'NavBarMain',
  props: {
    title: {
      default: "Login",
      type: String
    },
    id: {
      default: "NavBarMain",
      type: String
    }
  },
  data: function(){
    return{
      checkedcsv: true,
      checkedtmp: true
    }
  },
  methods:{

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
