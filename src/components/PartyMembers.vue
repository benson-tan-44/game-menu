<template>
  <div class="col-sm-6 col-md-4">
    <div class="panel panel-info">
      <div class="panel-heading">
        <h3 class="panel-title">
          <strong>{{part.name}}</strong>
        </h3>
      </div>
      <div class="panel-body">
        {{part.desc}}
        <button v-if="!edit" @click="edit = !edit" class="btn btn-primary">Edit Description</button>
        <div v-if="edit">
            <textarea v-model="inputDesc" type="text" />

            <span class="text-center">
            <button class="btn btn-success" @click="saveDesc">Confirm</button>
            <button class="btn btn-danger" @click="edit = !edit">Cancel</button>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      edit: false,
      inputDesc: ''
    }
  },
  props:['part'],
  methods: {
    saveDesc(){
      this.edit = false;

      const member = {
        id: this.part.id,
        desc: this.inputDesc
      };

      this.$store.dispatch('initDesc', member);
    }
  }

}



</script>

<style scoped>
textarea{
  overflow:hidden;
padding:10px;
width:250px;
height:200px;
font-size:14px;
margin:30px auto;
display:block;
border:1px solid #ccc;
resize:vertical;
}
</style>
