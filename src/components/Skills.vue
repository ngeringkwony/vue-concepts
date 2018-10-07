<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter a skill you have..." v-model="skill" v-validate="'min:5'" name="skill"/>
        <p class="alert" v-if="errors.has('skill')">{{errors.first('skill')}}</p>
        <!-- <input type="checkbox" id="checkbox" v-model="checked"> -->
      </form>

      <ul>
        <li v-for="(data, index) in skills" :key='index'>{{index}}. {{data.skill}}</li>
      </ul>

      <p>These are the skills you possess</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      skills: [
        {"skill": "Vue.js"},
        {"skill": "sass"},
        {"skill": "SVG Animation"}
      ],
      skill: "",
      // checked: false
    }
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then((result) => {
        if(result) {
          this.skills.push({skill: this.skill});
        this.skill = '';
        }else {
          console.log("Input not valid");
        }
      });
      // this.checked ? this.skills.push({skill: this.skill}) : this.skills.push({skill: 'LIAR'});
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only
  Components defined in a different file like skills.vue in this case wont be affected
  by "scoped" css -->

  <!--link to an external css file by adding "src=" -->
<style scoped>
  .holder {
    background: #fff;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }

   input {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
  }
  .alert {
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }

</style>
