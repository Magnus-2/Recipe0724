<template>
  <html lang="en">
<head>
	<meta charset="utf-8">
	<meta name="author" content="Kodinger">
	<meta name="viewport" content="width=device-width,initial-scale=1">
	<title>Sign Up</title>
</head>
    <body class="my-login-page">
	<section class="h-100">
		<div class="container h-100">
			<div class="row justify-content-md-center h-100">
				<div class="card-wrapper">
					<div class="brand">
                        <!-- Logo -->
						<img src="../assets/imgs/logo.png" alt="bootstrap 4 login page">
					</div>
					<div class="card fat">
						<div class="card-body">
							<h4 class="card-title">Register</h4>

								<div class="form-group">
									<label for="name">Name</label>
                  <!--Input field to store user entry for their username-->
									<input id="name" type="text" class="form-control" name="name" placeholder="Username" v-model="formData.username" required autofocus>
									<div class="invalid-feedback">
										What's your name?
									</div>
								</div>

								<div class="form-group">
									<label for="email">E-Mail Address</label>
                  <!--Input field to store user entry for their email-->
									<input id="email" type="email" class="form-control" name="email" placeholder="email" v-model="formData.email" required>
									<div class="invalid-feedback">
										Your email is invalid
									</div>
								</div>
                

								<div class="form-group">
									<label for="password">Password</label>
                  <!--Input field to store user entry for their password-->
									<input id="password" type="password" class="form-control" name="password" placeholder="password" v-model="formData.password" required data-eye>
									<div class="invalid-feedback">
										Password is required
									</div>
								</div>
                                <p style="color: black">Choose your Orientation</p>
                                <!-- Dropdown menu for user to select their form of diet -->
                                <select  class="form-select" aria-label="Default select example" v-model="formData.diet">
                                    <!-- <option selected>Orientation</option> -->
                                    <option value="Unrestricted">Unrestricted</option>
                                    <option value="Vegan">Vegan</option>
                                    <option value="Vegetarian">Vegetarian</option>
                                    <option value="Helal">Helal</option>
                                  </select>


								<!-- <div class="form-group">
									<div class="custom-checkbox custom-control">
										<input type="checkbox" name="agree" id="agree" class="custom-control-input" required="">
										<label for="agree" class="custom-control-label">I agree to the <a href="#">Terms and Conditions</a></label>
										<div class="invalid-feedback">
											You must agree with our Terms and Conditions
										</div>
									</div>
								</div> --> <br><br>

								<div class="form-group m-0">
                  <!--Through the click on the signup button the functions addUser and signUp get executed -->
                  <button id="signinbutton" @click="addUser(), signUp() " class=" btn btn-success " >SignUp</button>
								</div>
								<div class="mt-4 text-center">
                  <!--routerlink to redirect to the sign in page if user already has an account-->                  
                  <router-link to="/signin">
                      <a id="text"> Already have an account? &nbsp; </a> <button class="btn btn-success" id="createonebutton" role="button">Sign In</button>
                  </router-link>
								</div>
							
						</div>
					</div>
					<div class="footer">
						Copyright &copy; 2023 &mdash; Recipes finder
					</div>
				</div>
			</div>
		</div>
	</section>
</body>
    </html>
</template>
<script>
import{getAuth, createUserWithEmailAndPassword} from "firebase/auth"
import {getFirestore, addDoc, collection} from 'firebase/firestore'
export default {
  name: 'SignUp',
  data () {
    return {
      //store user information in formData details
      formData: {
        email: '',
        password: '',
        username:'',
        diet:'',
      }
    }
  },
  methods: {
    //method to access firebase authenticator to create a uer with their email and password 
    //in order to securely store and manage them 
    signUp () {
      console.log('SignUp')
      const auth = getAuth()
            createUserWithEmailAndPassword(
                auth,
                this.formData.email,
                this.formData.password
            )
            .then((userCredential)=>{
                console.log("Successfully registered!")
                this.$router.replace('/recipes')
            })
            .catch((error) => {
                console.log(error.code)
                alert(error.message)
            })
            
        }, 
        //addUser is a function to add the Users into the database but without their password
        //this way their password stays protected and we can still retrieve data about
        //their diet as well as their username or in future updates of the website even more details
        //about favorite recipes etc.
       async addUser(){
           const db = getFirestore()
           const docRef = await addDoc(collection(db, "User"), {
            Email: this.formData.email,
            Diet: this.formData.diet,
            Username: this.formData.username
          });
            console.log("Document written with ID: ", docRef.id);}}}
        

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import '../assets/css/login.css';
@import url("https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css");  
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>