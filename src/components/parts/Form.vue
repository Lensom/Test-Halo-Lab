<template>
  <div class="form__wrapper">
    <form id="form" class="form" @submit.prevent="checkForm" action="#" method="post">
      <div class="form__row--column">
        <div class="form__row">
          <label for="name" class="text--md">Your company name</label>
          <div class="input__wrapper">
            <input
              ref="textRef"
              id="name"
              class="input"
              v-model="userData.name"
              type="text"
              name="name"
              placeholder="Type text"
            />
          </div>
        </div>

        <div class="form__row form__row--numbers">
          <label for="age" class="text--md">
            Number of people
            <span class="star">*</span>
          </label>
          <div class="input__wrapper">
            <input
              id="age"
              class="input req"
              v-model="userData.numberOfPeople"
              type="number"
              placeholder="1-99"
              name="age"
              min="1"
              max="99"
              @blur="checkNumber"
              
            />
          <span class="error__message">{{numberIsValid}}</span>
          </div>
        </div>
      </div>

      <div class="form__row">
        <label for="area" class="text--md">
          Business area
          <span class="star">*</span>
        </label>
        <div class="input__wrapper">
          <input
            id="area"
            class="input req"
            v-model="userData.area"
            placeholder="Design, Marketing, Development, etc."
            type="text"
            name="area"
            @blur="checkText"
            
          />
          <span class="error__message">{{errors.required}}</span>
        </div>
        
      </div>

      <div class="form__row">
        <label for="textarea" class="text--md">
          Description
          <span class="star">*</span>
        </label>
        <div class="input__wrapper input__wrapper--area">
          <textarea
            name="textarea"
            class="input input__area req"
            placeholder="Type text"
            v-model="userData.description"
            id="textarea"
            cols="30"
            rows="10"
            @blur="checkText"
            
          ></textarea>
        <span class="error__message">{{errors.required}}</span>
        </div>
      </div>

      <div class="form__row form__row--right">
        <inputFile  @files="getFilesData"/>
      </div>

      <div class="btn__wrapper">
        <input type="submit" class="btn btn__submit" value="Submit" />
      </div>
    </form>
  </div>
</template>

<script>
import inputFile from "@/components/components/inputFile.vue";

export default {
  data: function() {
    return {
      numberIsValid: 'This field in required',
      formValid: false,
      errors: {
        required: 'This field in required',
        number: 'Please enter number from 1 to 99',
        clear: ''
      },
      userData: {
        name: null,
        numberOfPeople: null,
        area: null,
        description: null,
        files: []
      }
    };
  },
  components: {
    inputFile
  },
  methods: {
    enableError(e, state = false) {
      return state ? e.target.parentNode.classList.remove('error') : e.target.parentNode.classList.add('error')
    },
    checkNumber(e) {
      let num = this.userData.numberOfPeople;

      if (num == null || num == '') {
        this.enableError(e);
        this.numberIsValid = this.errors.required
      } else if (num < 1 || num > 99) {
        this.enableError(e);
        this.numberIsValid = this.errors.number
      } else {
        this.enableError(e, true);
        this.numberIsValid = this.errors.clear;
      }

      //    return (num == null || num == '')
      //   ? this.numberIsValid = this.errors.required
      //   : num < 1 || num > 99 
      //   ? this.numberIsValid = this.errors.number
      //   : this.numberIsValid = this.errors.clear;
    },
    checkText(e) {
      return e.target.value
        ? e.target.parentNode.classList.remove("error")
        : e.target.parentNode.classList.add("error");
    },
    getFilesData(data) {
      this.userData.files = data.nameOfFiles
    },
    checkForm() {
      let req = document.querySelectorAll(".req");
      
      for (let i of req) {
        if (!i.value) i.parentNode.classList.add('error')
      }

      if (this.formValid) {
        console.group ( 'Customer message' );
        console.log(`Company name: ${this.userData.name}`)
        console.log(`Number of people: ${this.userData.numberOfPeople}`)
        console.log(`Business area: ${this.userData.area}`)
        console.log(`Description: ${this.userData.description}`)
        console.dir(`Files: ${this.userData.files}`)
        console.groupEnd()
      }
    }
  }
};
</script>
