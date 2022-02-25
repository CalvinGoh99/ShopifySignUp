<template>
  <div class="card-page-body">
        <div class="card-container">
            <div class="card-form-section">
                <div class="card-form">
                    <div class="card-header">
                        <div class="marketing-logo">
                            <img src="@/assets/shopify-logo.png"  class="shopify-logo">
                        </div>
                        <h1 class="card-heading">Create a Shopify ID</h1>
                        <h2 class="card-subheading">The ecommerce platform made for you</h2>
                    </div>
    
                    <div class="signup-form-section">
                        <form @submit.prevent="handleSubmit" @submit="validatePassword(this.password)"> 
                            <div class="signup-container">
                                <div class="signup-info">
                                    <label class="signup-label">Email</label>
                                    <input type="email" required v-model.trim="email" :maxlength="emailLength" class="signup-email">
                                </div>
    
                                <div class="fullname-info">
                                    <div class="fname-info">
                                        <label class="signup-label">First name</label>
                                        <input type="text" required v-model.trim="fname" :maxlength="nameLength" class="signup-fname">
                                    </div>
                                    <div class="lname-info">
                                        <label class="signup-label">Last name</label>
                                        <input type="text" required v-model.trim="lname" :maxlength="nameLength" class="signup-lname">
                                    </div>
                                </div>
    
                                <p class="help-info">Enter your first and last name as they appear on your government-issued ID.</p>
    
                                <div class="signup-info">
                                    <label class="signup-label">Password</label>
                                    <input @keyup="validatePassword(this.password)" type="password" required v-model="password" :maxlength="passwordLength" class="signup-password">
                                </div>

                                <div v-if="passwordError">    
                                    <p class="help-info">{{ passwordError }}</p>
                                </div>

                                <div class="signup-info">
                                    <label class="signup-label">Confirm new password</label>
                                    <input @keyup="Submit" type="password" required v-model="confirmPassword" :maxlength="passwordLength" class="signup-confirm-password">
                                </div>

                                <div v-if="confirmpasswordError">    
                                    <p class="help-info">{{ confirmpasswordError }}</p>
                                </div>

                                <div>    
                                    <button :class="{ signup: isSubmit , notsignup: notSubmit }" :disabled="isDisabled">Create Shopify ID</button>
                                </div>
                            </div>
                        </form>

                        <div class="more-info">
                            <p class="help-info">By proceeding, you agree to the <a href="#">Terms and Conditions</a></p>
                            <p class="help-info">Already have a Shopify ID? <a href="./login.html">Log in</a></p>
                        </div>
                    </div>
                </div>
            </div>

            <footer class="card-footer">
                <a class="more-info-footer">Help</a>
                <a class="more-info-footer">Privacy</a>
                <a class="more-info-footer">Terms</a>
            </footer>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            email: '',
            fname: '',
            lname: '',
            password: '',
            confirmPassword: '',
            emailLength: 40,
            nameLength: 15,
            passwordLength: 25,
            passwordError: '',
            confirmpasswordError: '',
            isSubmit: false,
            notSubmit: true,
            isDisabled: true
        }
    },
    methods:{
        handleSubmit(){
            if(this.passwordError=='' && this.confirmpasswordError==''){
                console.log('Email: ', this.email)
                console.log('First name: ', this.fname)
                console.log('Last name: ', this.lname)
                console.log('Password: ', this.password)
                console.log('Confirm password: ', this.confirmPassword)
            }
        },

        validatePassword(password){

            let trimPassword = password.trim()
            if(password != trimPassword){
                this.passwordError = 'Your password can’t begin or end with a space.'                    
            }else if(this.password.length < 6){
                this.passwordError = 'Your password must be at least 5 characters'     
                if(this.password.length >= 5){
                    this.passwordError = ''
                }          
            }else{
                this.passwordError = ''
            }  
        },

        Submit(){

            if(this.password != this.confirmPassword){
                this.confirmpasswordError = 'Confirm password must be same as password.'
            }else{
                this.confirmpasswordError = ''
                this.isDisabled = false
            }

            if(this.email != '' && this.fname != '' && this.lname != '' && this.password != '' && this.confirmPassword != ''){
                this.isSubmit = true
                this.notSubmit = false
                this.isDisabled = false

            }else if(this.email == '' || this.fname == '' || this.lname =='' || this.password == '' || this.confirmPassword == ''){
                this.notSubmit = true
                this.isSubmit = false
                this.isDisabled = true
            }
        },
    }
}
</script>

<style>

*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

a{
    text-decoration: none;
}

body{
    line-height: 1.3;
    background-color: #084c3f;
    font-family: 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
}

/* Page entire body */
.card-page-body{
    display: flex;
    min-height: 100vh;
    justify-content: center;
    flex-direction: column;
    align-items: flex-start;
}

/* Card container */
.card-container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: #ffffff;
    border-radius: 8px;
    margin: 2vw 10vw;
    width: 100%;
    max-width: 33rem;
}

/* Container header */

.shopify-logo{
    display: inline-block;
    position: relative;
    width: 120px;
    height: 35px;
}

.card-form-section{
    display: block;
    width: 100%;
    padding: 4em 2.5em 0;
}

.marketing-logo{
    margin-bottom: 3em;
}

.card-header{
    padding-left: 8px;
}

.card-heading{
    font-weight: 500;
    font-size: 1.5rem;
    margin-bottom: 5px;
}

.card-subheading{
    font-weight: 400;
    color: #6d7175;
    font-size: 1em;
    margin-bottom: 20px;
}

/* Help section */

.help-info{
    display: block;
    font-size: 0.9em;
    color: #48525f;
    margin-bottom: 10px;
}

.help-info a{
    text-decoration: none;
    color: #008161;
}

.help-info a:hover{
    text-decoration: underline;
    color: #014e3b;
}

/* Container footer */

.card-footer{
    display: flex;
    justify-content: flex-end;
    padding: 2.5rem 1.5rem 2.5rem 2rem;
}

.card-footer a{
    padding: 0 1em;
    font-size: 0.9rem;
    font-weight: 500;
    cursor: pointer;
    color: #5f6f7c;
}

.card-footer a:hover{
    text-decoration: underline;
    color: #3d474e;
}

/* Signup form */

.signup-form-section{
    display: flex;
    flex-wrap: wrap;
    width: 100%;
}

.signup-container, .more-info{
    display: block;
    width: 100%;
}

.signup-info, .fname-info, .lname-info{
    display: inline-flex;
    flex-direction: column;
    width: 100%;
    padding: 12px 8px;
}

.fullname-info{
    display: flex;
    flex-wrap: wrap;
    width: 100%;
}

.fname-info, .lname-info{
    width: 50%;
}

.signup-label{
    padding-bottom: 5px;
}

input{
    font-size: 1rem;
    padding: 1rem;
    background-color: #ffffff;
    border: 0.05rem solid #90959b;
    border-radius: 4px;
    outline-color: #01684e;
}

p{
    padding: 0px 8px;
}

.notsignup{
    display: block;
    position: relative;
    align-items: center;
    width: 100%;
    font-size: 0.95rem;
    font-weight: 700;
    color: #83878d;
    background-color: #f1f1f1;
    border: none;
    border-radius: 4px;
    cursor: normal;
    padding: 1.8rem 3.5rem;
    margin: 20px 0px;
    z-index: 1;
}

.signup{
    display: block;
    position: relative;
    align-items: center;
    width: 100%;
    font-size: 0.95rem;
    font-weight: 700;
    color: #ffffff;
    background-color: #027e5f;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    padding: 1.8rem 3.5rem;
    margin: 20px 0px;
    z-index: 1;
}

</style>