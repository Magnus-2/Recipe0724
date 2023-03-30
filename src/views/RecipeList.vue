<template>
  <html lang="en">
<head>
	<meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="description" content="Start your development with Dorang landing page.">
    <meta name="author" content="Devcrud">
    <title>Recipe List</title>


</head>
<body

    data-spy="scroll"
    data-target=".navbar"
    data-offset="40"
    id="home"
    class="dark-theme">

    <div class="background-overlay">

    <div class="container page-container">
        <div class="col-md-10 col-lg-8 m-auto">
            <h3 class="title mb-4">Recipes</h3>
        </div>
      <br/>
        
      <button class="btn btn-success search-btn" style="font-size: larger; border-style: solid; border-color: rgb(0, 64, 102);  background-color: rgb(0, 64, 102);"><a href="findrecipes">Search Recipes</a></button>
        <br/><br/>
     <!-- row with some recipe  -->
     <div class="row mb-5">
    <div class="col-md-6" v-for="(recipe, key) in recipes" :key='key'>
            <img v-bind:src="`../src/assets/imgs/${recipe.image}`" width="400" height="300" alt="pic">
                <div class="card-body">
                    <h3 class="card-title"><p class="recipename" >{{recipe.Recipe_Name}}</p></h3>
                    <router-link
                            :to="{path: 'info', name: 'Info', params:{recipe:recipe.Recipe_Name}}">
                            <button class="btn btn-success" role="button">See Recipe</button>
                        </router-link>
                </div>
            
        </div>   
        </div>  <!-- end of row -->
      </div>
      
            <footer class="footer">
                <p class="infos">&copy;, Made with <i class="ti-heart text-danger"></i> by Celina, Magnus, Till and Kevin</p>       
                <span>|</span>  
                <div class="links">
                    <a href="#">About</a>
                    <a href="#">Recipe</a>
                    <a href="#">Profile</a>
                    <button @click="logout" class="btn btn-default" style="color: red; border: solid; background-color: black; font-weight: 700;">Logout</button>
                </div>

                    
             
            </footer>
          </div>
</body>


          
    </html>
  </template>
  
  <script>
  import {collection, onSnapshot, doc, getFirestore, } from "firebase/firestore"
  import {getAuth, signOut} from 'firebase/auth'
  export default {
    name: 'RecipeList',
    data () {
      return {
        recipe: null,
        //store the recipe data in here to access in the html template 
        recipes: {},
       
        
        auth: getAuth()
      }
    },
    mounted () {
      //access the Recipe database to retrieve recipe data
      console.log('Recipe List')
      const db = getFirestore()
      const colRef = collection(db, "Recipe")
      onSnapshot(colRef, snapShot => {
        //store the retrieved data in the recipes object
        this.recipes = snapShot.docs.map(doc => doc.data())
        
      })  
    },
    methods: {
      //deactivate the authorization through the logout button
      logout () {
        console.log('logout')
        signOut(this.auth)
      //after logout redirect to the signin page
      .then(()=>{
        this.$router.replace('/signin')
      })
      //if logout didn't work, display the error message
      .catch((error) => {
        alert(error.message)
      })
      }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  h1, h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    /* display: inline-block; */
    margin: 0 10px;
  }
  a {
    color: #ffffff;
  }
  p.citydetail{
    text-align: justify;
  }


.background-overlay {
  position: relative;
  background-image: url("https://www.fuchs.de/wp-content/uploads/2017/11/thanksgiving.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}

.background-overlay:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0,0,0,0.7);
}
.search-btn {
  position: relative;
  z-index: 9999;
}
  </style>