<template>
    <form @submit.prevent="handleSubmit">
        <label for="email">Email</label>
        <input type="email" required v-model="email">
 
        <label for="password">Password</label>
        <input type="password" required v-model="password">
        <div class="error" v-if="passwordError">{{ passwordError }}</div>

        <label for="role">Role</label>
        <select v-model="role" id="role" required>
            <option value="">-- select role --</option>
        </select>

        <label for="tempSkills">Skills</label>
        <input type="text" v-model="tempSkills" @keyup.alt="addSkill">
        <div v-for="skill in skills" class="pill">
            <span @click="removeSkill(skill)">{{ skill }}</span>
        </div>

        <div class="terms">
            <input type="checkbox" required v-model="terms">
            <label>Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button type="submit">Create an Account</button>
        </div>
        <!-- <div>
        <input type="checkbox" value="Mhmd" v-model="names">
        <label>Mhmd</label>
        
        <input type="checkbox" value="sobhi" v-model="names">
        <label>sobhi</label>
        
        <input type="checkbox" value="ghazal" v-model="names">
        <label>ghazal</label>
        
        <input type="checkbox" value="khaled" v-model="names">
        <label>khaled</label>
    </div> -->
    </form>
    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ roleList.find((b) => b.value === role)?.text || 'None' }}</p>
    <p>Terms Accepted: {{ terms }}</p>
    <!-- <p>Names: {{ names }}</p> -->
</template>

<script>
export default {
    data() {
        return {
            email: 'sobhi',
            password: '',
            role: '',
            terms: false,
            roleList: [{ value: 'developer', text: 'Web Developer' }, { value: 'designer', text: 'Web Designer' }],
            // names: [],
            tempSkills: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        importRoleList() {
            var roleInput = document.getElementById("role");
            this.roleList.forEach(element => {
                var option = document.createElement("option");
                option.value = element.value;
                option.text = element.text;
                roleInput.add(option);
            });
        },
        addSkill(e) {
            if (e.key === ',' && this.tempSkills) {
                if (!this.skills.includes(this.tempSkills)) {
                    this.skills.push(this.tempSkills)
                }
                this.tempSkills = ''
            }
        },
        removeSkill(skill) {
           // this.skills.splice(this.skills.indexOf(skill), 1)
            this.skills = this.skills.filter((b) => { return b !== skill })
        },
        handleSubmit() {
            console.log('form submitted')
            //validate some props
            this.passwordError=this.password.length > 5 ? '' : 'Password must be at leat 6 charactor'
        }
    },
    mounted() {
        this.importRoleList()
    }
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input,
select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    color: white;
    border-radius: 20px;
}
.submit {
    text-align: center;
}
.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>