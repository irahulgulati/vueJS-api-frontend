<template>
  <div id="app container">
    <patients v-bind:patientdata="patientdata" v-on:delrecord="deleteRecord"/>
  </div>
</template>

<script>
import patients from '../components/patients.vue'
import axios from 'axios'
export default {
  name: 'App',
  components: {
    patients
  },
  data(){
    return {
      patientdata : []
    }
  },
  methods : {
    fetchCustomers(){
      axios.get('http://3.133.84.56/api/patients')
        .then(res=>this.patientdata=res.data)
        .catch(err=>console.log(err))
      
      
    },
    createPatient(newPatient){
      console.log(newPatient)
      const {location,streetname,status} = newPatient;
      const name = newPatient.name.toLowerCase();
      axios.post('http://3.133.84.56/api/patients',{
        name,
        location,
        streetname,
        status
      }).then(res=>{
        if(res.data.name == "patient already exists"){
          alert("Patient already exists")
        }
        else{
          this.patientdata=[...this.patientdata,res.data]
        }
      })
        .catch(err=>console.log(err))
    },
    deleteRecord (id){
      axios.delete(`http://3.133.84.56/api/patients/${id}`)
      .then(this.patientdata=this.patientdata.filter(patientdata=>patientdata.id!==id))
      .catch(err=>console.log(err))
    }
  },
  created: function(){
    this.fetchCustomers();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
