<template>
  <div class="about">
    <addpatient v-on:newPatient="createPatient"/>
  </div>
</template>
<script>
import addpatient from '../components/addpatient.vue'
import axios from 'axios'
export default {
  name: 'create',
  components: {
    addpatient
  },
  methods : {
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
    }
}
}
</script>

