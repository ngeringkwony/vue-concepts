<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter a skill you have..." v-model="skill" v-validate="'min:5'" name="skill"/>        <!-- <input type="checkbox" id="checkbox" v-model="checked"> -->
        <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutY">
          <p class="alert" v-if="errors.has('skill')">{{errors.first('skill')}}</p>
        </transition>
      </form>

      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key='index'>
            {{index + 1}}. {{data.skill}}

            <i class="fas fa-trash-alt" v-on:click="remove(index)"></i>
            </li>
        </transition-group>
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
    },
    remove(i) {
      this.skills.splice(i, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only
  Components defined in a different file like skills.vue in this case wont be affected
  by "scoped" css -->

  <!--link to an external css file by adding "src=" -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1"; /*imported library for animations*/
@import "https://use.fontawesome.com/releases/v5.3.1/css/all.css"; /*font-awesome delete icon*/

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

  .alert-in-enter-active {
    animation: bounce-in .7s ease;
  }
  .alert-in-leave-active {
    animation: bounce-in .7s ease reverse;
  }

  i {
    float: right;
  }

  @keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}

</style>
