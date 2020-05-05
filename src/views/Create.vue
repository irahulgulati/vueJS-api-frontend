<template>
  <div class="about">
    <div class="codehandler" v-if="code">
        {{code}}
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
      code:''
    }
  },
  methods : {
    createPatient(newPatient){
      const {location,streetname,status} = newPatient;
      const name = newPatient.name.toLowerCase();
      this.code="Processing request"
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
                  this.code = "Patient already exists"
                  }
                else{
                  this.patientdata=[...this.patientdata,res.data]
                  this.code="Patient record added to database"
                }
             })
            .catch(() => this.code = 'urrrghhhh! Record cannot be created')
           }
        )
      .catch(() => {
        this.code="404! Connection timed out";
        })
      
    }
}
}
</script>

