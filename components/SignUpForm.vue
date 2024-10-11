<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
      <option value="software">Software Developer</option>
      <option value="dataeng">Data Engineer</option>
    </select>

    <div>
      <h6 class="colorme">Highest Education:</h6>
      <input type="checkbox" v-model="education" value="degree">
      <label>Bachelor's Degree in Engineering</label>
    </div>
     <div>
      <input type="checkbox" v-model="education" value="pg">
      <label>Post Graduation</label>
    </div>
    <div>
      <input type="checkbox" v-model="education" value="deploma">
      <label>Deploma</label>
    </div>
    <label>Skills: </label><span class="sosmall">* Just Press Enter after each skill</span>
    <input type="text" v-model="tempSkill" @keydown.enter.prevent="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="RemoveSkill(skill)">{{ skill }} </span>
    </div>
    <hr>
    <div class="terms">
    <input type="checkbox" required v-model="terms">
    <label> Accept Terms and Conditions</label>
    </div>
    <div class="submit">
    <button>Create Account </button>
    </div>
  </form>

</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'developer',
      terms: false,
      education: [],
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
      if (this.tempSkill.trim() !== '') {
      if (!this.skills.includes(this.tempSkill.trim())) {
        this.skills.push(this.tempSkill.trim());
      }
      this.tempSkill = ''; // Clear the input after adding
      }
    },
    RemoveSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    handleSubmit() {
      //Validate Password
      this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'
      if(!this.passwordError) {
        //code to store in database will be here
        console.log(this.email)
        console.log(this.password)
        console.log(this.role)
        console.log(this.terms)
        console.log(this.education)
        console.log(this.skills)

      }
    }
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
  input, select {
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
    top: 2px;
  }
  h6.colorme {
    letter-spacing: 1px;
    font-weight: bold;
    color: #aaa;
    text-transform: uppercase;
    font-size: 0.6em;
    margin: 25px 0 15px;
}
span.sosmall {
    font-size: 10px;
    color: #aaa;
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
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
    font-size: 0.8em;
    color: #b81414;
    margin: 10px 0px;
    font-weight: bold;
}
</style>