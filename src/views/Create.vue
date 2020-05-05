<template>
  <div class="about">
    <div class="errorhandler" v-if="error">
        {{error}}
    </div>
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
  data(){
    return {
      error:''
    }
  },
  methods : {
    createPatient(newPatient){
      const {location,streetname,status} = newPatient;
      const name = newPatient.name.toLowerCase();
      axios.get('http://3.133.84.56/api/patients')
      .then(
          () => {
            axios.post('http://3.133.84.56/api/patients',{
              name,
              location,
              streetname,
              status
            })
            .then(res=>{
                if(res.data.name == "patient already exists"){
                  this.error = "Patient already exists"
                  }
                else{
                  this.patientdata=[...this.patientdata,res.data]
                }
             })
            .catch(() => this.error = 'urrrghhhh! Record cannot be created')
           }
        )
      .catch(() => this.error="404! Connection timed out")
      
    }
}
}
</script>

