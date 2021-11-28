<template>
    <form @submit.prevent="handleSubmit">
        <label for="email">Email</label>
        <input type="email" required id="email" v-model="email">
        <label for="password">Password</label>
        <input type="password" required id="password" v-model="password">
        <div v-if="passwordError" class="error">
            {{ passwordError }}
        </div>
        <label for="role">Role</label>
        <select name="role" id="role" v-model="role">
            <option value="dev">Web Developer</option>
            <option value="designer">UI/UX Designer</option>
        </select>

        <label for="skills">Skills:</label>
        <input type="text" id='skills' v-model="tempskill" @keyup.alt="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill" @click="deleteSkill(skill)">
            {{ skill }}
        </div>

        <div class="terms">
            <input type="checkbox" required v-model="terms">
            <label for="">Accept terms & conditions</label>
        </div>
        <div class="terms">
            <input type="checkbox" value="JD" required v-model="names">
            <label for="">JD</label>
        </div>
        <div class="terms">
            <input type="checkbox" value="Deo" required v-model="names">
            <label for="">Deo</label>
        </div>

        <div class="submit">
            <button type="submit">Create an Account</button>
        </div>
    </form>

    <p>email: {{ email }}</p>
    <p>password: {{ password }}</p>
    <p>role: {{ role }}</p>
    <p>terms: {{ terms }}</p>
    <p>names: {{ names }}</p>
    
</template>
<script>
export default {
    data(){
        return{
            email:'',
            password:'',
            role:'',
            terms: false,
            names:[],
            tempskill:'',
            skills:[],
            passwordError:''
        }
    },
    methods:{
        addSkill(e){
            if(e.key === ',' && this.tempskill){
                if(!this.skills.includes(this.tempskill)){
                    this.skills.push(this.tempskill)
                }
                this.tempskill = ''
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter( s => ( s !== skill ))
        },
        handleSubmit(){
            //password validation
            this.passwordError = this.password.length > 5 ?
            '': 'password must be atleast 6 characters'

            if(!this.passwordError){
                console.log(this.email)
                console.log(this.password)
                console.log(this.role)
                console.log(this.terms)
                console.log(this.names)
            }
        }
    }
}
</script>
<style>
    form{
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top:2px
    }
    select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    .pill{
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor:pointer;
    }
    button{
        background: #0b6dff;
        border: none;
        padding: 10px 20px;
        color: white;
        margin-top:20px;
        border-radius: 20px
    }
    .submit{
        text-align: center;
    }
    .error{
        color: #ff0862;
        margin-top: 10px;
        font-size: 0.8rem;
        font-weight: bold;
    }
</style>