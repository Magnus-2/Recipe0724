<template>
<div class="AddRecipes"></div>
    <div class="row">
            <h2>Signin</h2>
           
            <div class="col-xs-6 col-sm-6 col-md-6 col-lg-6 col-md-offset-3">

                <input type="email" class="form-control" placeholder="email" v-model="formData.email">
                <br>
                <input type="password" class="form-control" placeholder="password" v-model="formData.password">
                <br>
                <button @click="signIn" class="btn btn-success btn-block full-width" >Signin</button>
            </div>

    </div>

</template>

<script>
// export default{
//     name:AddRecipes,
//     data(){
//         return{recipe:{
//             instructions:'',
//             recipeId:{},
//             recipeName:'',
//             Servings: '',
//             Style:'',
//             Total_Carbs:'',
//             Total_Fats:'',
//             Total_Protein:'',
//             Total_kcal:'',
//             User_ID_Publisher:getUserId()

        
//         },

//         }
            
//         }
//     }



// async addUser(){
//            const db = getFirestore()
//            const docRef = await addDoc(collection(db, "User"), {
//             Email: this.formData.email,
//             Diet: this.formData.diet,
//             Username: this.formData.username
//           });
//             console.log("Document written with ID: ", docRef.id);}
        



</script>