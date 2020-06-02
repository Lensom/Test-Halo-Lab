<template>
  <div class="form__wrapper">
    <form id="form" class="form" @submit="checkForm" action="#" method="post">
      <div class="form__row--column">
        <div class="form__row">
          <label for="name" class="text--md">Your company name</label>
          <div class="input__wrapper">
            <input
              ref="textRef"
              id="name"
              class="input"
              v-model="name"
              type="text"
              name="name"
              required
              @blur="checkText"
              placeholder="Type text"
            />
          </div>
        </div>

        <div class="form__row form__row--numbers" :class="{'error': ageIsValid}">
          <label for="age" class="text--md">
            Number of people
            <span class="star">*</span>
          </label>
          <div class="input__wrapper">
            <input
              id="age"
              class="input"
              v-model="age"
              type="number"
              placeholder="1-99"
              name="age"
              min="1"
              max="99"
              @blur="checkAge"
              required
            />
          </div>
          <span class="error__message" v-if="ageIsValid">This field in required</span>
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
            class="input"
            v-model="area"
            placeholder="Design, Marketing, Development, etc."
            type="text"
            name="area"
            @blur="checkText"
            required
          />
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
            class="input input__area"
            placeholder="Type text"
            v-model="textarea"
            id="textarea"
            cols="30"
            rows="10"
            @blur="checkText"
          ></textarea>
        </div>
      </div>

      <div class="form__row form__row--right">
        <inputFile />
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
      name: null,
      age: null,
      ageIsValid: false,
      area: null,
      textarea: null,
      errors: ["This field in required", "Please enter number from 1 to 99"]
    };
  },
  components: {
    inputFile
  },
  methods: {
    checkAge() {
      return this.age < 1 || this.age > 99
        ? (this.ageIsValid = true)
        : (this.ageIsValid = false);
    },
    checkText(e) {
      return e.target.value
        ? e.target.parentNode.classList.remove("error")
        : e.target.parentNode.classList.add("error");
    },
    checkForm() {}
  }
};
</script>
