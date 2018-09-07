<template>
  <div class="hello">
    <div class='holder'>
      <form @submit.prevent="addSkill">
        <input type='text' placeholder='enter a skill you have' v-model="skill" v-validate="'min:5'" name="skill"/> <br/>
        <p class="alert" v-if="errors.has('skill')"> The skill field must be atleast 5 chars </p>
      </form>
      {{skill}}
      <ul>
        <li v-for="(data,index) in skills" :key='data.skill'>
        {{index}}. {{data.skill}}
        </li>
      </ul>
      <p> These are the skills you have </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      skill:"",
      skills: [{ skill: 'vuejs' }, { skill: 'frontend' }],
    }
  },
  methods:{
    addSkill(){
      this.$validator.validateAll().then(result => {
        if(result) {
          this.skills.push({skill:this.skill})
          this.skill = ''
        }
      })

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
