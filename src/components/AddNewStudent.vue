<template>
    <div>        
        <form @submit.prevent="register" >  
        <div class="container">  
  <center>  <h1> Student Registeration Form</h1> </center>  
  <hr>  
  <label> Firstname </label>   
<input type="text" name="firstname" placeholder= "Firstname" size="15" required v-model="firstname"/> 

<label> Lastname: </label>    
<input type="text" name="lastname" placeholder="Lastname" size="15" required v-model="lastname" />   

<div>  
<label>   
Course :  
</label>   
  
<select v-model="course">  
<option disabled value="" >Course</option>  
<option value="SE">SE</option>  
<option value="QA">QA</option>  
<option value="BA">BA</option>  
 
</select>  
</div>  
<div>  
<label>   
Gender :  
</label><br>  
<input type="radio" value="Male" name="gender" checked v-model="gender"> Male   
<input type="radio" value="Female" name="gender" v-model="gender"> Female   
<input type="radio" value="Other" name="gender" v-model="gender"> Other  
  
</div>  
<label>   
Phone :  
</label>  
<input type="text" name="phone" placeholder="phone no." size="10" required v-model="phone">   

Current Address :  
<textarea cols="80" rows="5" placeholder="Current Address" value="address" required v-model="address">  
</textarea>  
 <label for="email"><b>Email</b></label>  
 <input type="text" placeholder="Enter Email" name="email" required v-model="email">  
  
    
    <button type="submit" class="registerbtn" >Register</button>    
    </div>
</form>  
<p>{{firstname}}--{{ lastname }}</p>
</div>
   
</template>

<script>
import axios from 'axios';



export default {
    data(){
        return{
            firstname:'',
            lastname:'',
            course:'',
            gender:'',
            phone:'',
            address:'',
            email:'',

            
        }
    },
    methods:{
        register(){
            console.log(this.firstname),
            console.log(this.lastname)

            const users={
                "fname":this.firstname,
                "lname":this.lastname,
                "course":this.course,
                "gender":this.gender,
                "phone":this.phone,
                "address":this.address,
                "email":this.email
            }
            
    axios.post('http://localhost:3000/users', users)
  .then(response => {
    console.log('Data was successfully written to the JSON Server endpoint!');
    console.log(response.data); // The data that was written to the endpoint

    this.firstname = '';
          this.lastname = '';
          this.course = '';
          this.gender = '';
          this.phone = '';
          this.address = '';
          this.email = '';

  })
  .catch(error => {
    console.error('An error occurred while writing data to the JSON Server endpoint.');
    console.error(error);
  });

        }
    }
}

</script>


<style scoped>
form{
    max-width: 420px;
    margin: 30px auto;
    background: rgb(211, 208, 208);
}
.container {  
    padding: 50px;  
  /* background-color: rgb(63, 64, 65);   */
}  
  
input[type=text], input[type=password], textarea {  
  width: 100%;  
  padding: 15px;  
  margin: 5px 0 22px 0;  
  display: inline-block;  
  border: none;  
  background: #f1f1f1;  
}  
input[type=text]:focus, input[type=password]:focus {  
  background-color: rgb(223, 247, 247);  
  outline: none;  
}  
 div {  
            padding: 10px 0;  
         }  
hr {  
  border: 1px solid #f1f1f1;  
  margin-bottom: 25px;  
}  
.registerbtn {  
  background-color: #889e89;  
  color: white;  
  padding: 16px 20px;  
  margin: 8px 0;  
  border: none;  
  cursor: pointer;  
  width: 100%;  
  opacity: 0.9;  
}  
.registerbtn:hover {  
  opacity: 1;  
}  
</style>