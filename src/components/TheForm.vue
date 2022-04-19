<template>
  <form v-on:submit.prevent="submitForm">
    <h1>Using Forms in Vuejs</h1>
    <div
      class="form-control"
      :class="{ invalid: userNameValidity === 'invalid' }"
    >
      <label for="user-name">Your Name</label>
      <input
        id="user-name"
        name="user-name"
        type="text"
        v-model.trim="userName"
        v-on:blur="validateInput"
      />
      <!-- blur event is fired when the input filed loses its focus  -->
      <small v-if="userNameValidity === 'invalid'"
        >*Please enter a valid name</small
      >
    </div>
    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <input id="age" name="age" type="number" v-model.number="userAge" />
    </div>
    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select
        id="referrer"
        name="referrer"
        v-model="referrer"
        v-on:change="handelSelectOptionChanges"
      >
        <option disabled value="">Please select one</option>
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <input
          id="interest-news"
          name="interest"
          type="checkbox"
          value="news"
          v-model="interest"
        />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input
          id="interest-tutorials"
          name="interest"
          type="checkbox"
          value="tutorial"
          v-model="interest"
        />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input
          id="interest-nothing"
          name="interest"
          type="checkbox"
          value="nothing"
          v-model="interest"
        />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input
          id="how-video"
          name="how"
          type="radio"
          value="video"
          v-model="how"
        />
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input
          id="how-blogs"
          name="how"
          type="radio"
          value="blogs"
          v-model="how"
        />
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input
          id="how-other"
          name="how"
          type="radio"
          value="other"
          v-model="how"
        />
        <label for="how-other">Other</label>
      </div>
    </div>
    <div class="form-control borderd">
      <h2>Rate our service:</h2>
      <!-- Custom Input Component -->
      <!-- 
        if you use v-model on a custom component, that is some thing supported by Vue
        and it will set a very specific prop 'modelValue' and it will listen to very specific event 'update:modelValue'
       -->
      <rating-control v-model:rate="rating"></rating-control>
    </div>
    <div class="form-control">
      <input
        type="checkbox"
        id="confirm-terms"
        name="confirm-terms"
        v-model="confirm"
        v-on:change="handelCheckBoxChanges"
        true-value="agree"
        false-value="not agree"
      />
      <label for="confirm-terms">Agree to terms of use?</label>
    </div>
    <div>
      <button>Save Data</button>
    </div>
  </form>
</template>

<script>
import RatingControl from './RatingControl.vue';
export default {
  components: { RatingControl },
  data() {
    return {
      userName: '',
      userAge: null,
      referrer: '',
      interest: [],
      how: null,
      confirm: 'not agree',
      rating: null,
      userNameValidity: 'pending',
    };
  },
  methods: {
    submitForm() {
      // TODO console log form data and clears input values
      alert('Submited');
      console.log('User Name', this.userName);
      this.userName = '';
      console.log('User Age', this.userAge);
      this.userAge = null;
      console.log(this.referrer);
      this.referrer = '';
      console.log('Interests in', this.interest);
      this.interest = [];
      console.log(this.how);
      this.how = null;
      console.log(this.confirm);
      this.confirm = false;
      console.log(this.rating);
      this.rating = null;
    },
    validateInput() {
      if (this.userName === '') {
        this.userNameValidity = 'invalid';
      } else {
        this.userNameValidity = 'valid';
      }
    },
    handelSelectOptionChanges(event) {
      // <select> use value as a prop and change as an event.
      console.log(event.target.value);
      console.log('Select Option Changed');
    },
    handelCheckBoxChanges(event) {
      /*
      <input type="checkbox"> and <input type="radio"> use checked property and
       change event;
      */
      console.log('Checkbox Changed');
      const el = event.target;

      if (el.checked) {
        console.log('I agree to terms for use');
      } else {
        console.log('I not agree to terms for use');
      }
    },
  },
};
</script>

<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

form h1 {
  text-align: center;
  color: #333;
  margin-top: 0;
}
.form-control {
  margin: 0.5rem 0;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label,
.form-control.invalid small {
  color: red;
}
.borderd {
  border: 1px solid #333;
  padding: 1rem;
  border-radius: 8px;
}
label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>
