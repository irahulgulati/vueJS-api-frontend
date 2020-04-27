<template>
    <div class="add ">
      <div class="container">
        <form @submit="addPatient">
          <div class="input-group ">
            <!-- <div class="input-group-prepend">
             <span class="input-group-text" id="">Patient's Details</span>
             </div> -->
             <input type="text" class="form-control" placeholder="Name" v-model="name">
             <input type="text" class="form-control" placeholder="Location" v-model="location">
             <input type="text" class="form-control" placeholder="Street" v-model="streetname">
             <input type="text" class="form-control" placeholder="Covid status" v-model="status">
             <input type="submit" value="Create Record" class="btn-primary sbmt">
        </div>
        </form>
      </div>
    </div>
</template>
<script>
export default {
    name: 'addpatient',
    data() {
        return {
            name: '',
            location: '',
            streetname:'',
            status:''
        }
        
    },
    methods: {
        addPatient(e){
            if(this.name !== ''&& this.location !== ''&& this.streetname !== ''&&this.status !== ''){
                            const newPatient = {
                name: this.name,
                location:this.location,
                streetname:this.streetname,
                status:this.status
            }
            this.$emit('newPatient',newPatient)
            this.name = ''
            this.location= '',
            this.streetname='',
            this.status=''
            }
            else{
                alert("Please enter all the details")
            }
            e.preventDefault();

            // console.log(newPatient)
            

        }
    }
    
}
</script>
<style scoped>
    .add{
        margin-bottom: 2em;

    }

    .sbmt{
        outline: none;
        border-top-right-radius:5px ;
        border-bottom-right-radius: 5px;
    }
</style>