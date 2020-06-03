<template>
  <form id="form" class="form" @submit.prevent="checkForm" action="#" method="post">
    <div class="form__row--column">
      <div class="form__row">
        <label for="name" class="text--md">Your company name</label>
        <div class="input">
          <input
            id="name"
            class="input__field"
            v-model="inputUserName.value"
            type="text"
            name="name"
            :placeholder="inputUserName.placeholder"
          />
        </div>
      </div>

      <div class="form__row form__row--numbers">
        <label for="age" class="text--md">
          Number of people
          <span class="star">*</span>
        </label>
        <div
          class="input"
          :class="{error:  inputNumberOfPeople.isValid!==null && !inputNumberOfPeople.isValid}"
        >
          <input
            id="age"
            class="input__field req"
            v-model.number="inputNumberOfPeople.value"
            type="number"
            :placeholder="inputNumberOfPeople.placeholder"
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
      <div class="input" :class="{error:  inputArea.isValid!==null && !inputArea.isValid} ">
        <input
          id="area"
          class="input__field req"
          v-model="inputArea.value"
          :placeholder="inputArea.placeholder"
          type="text"
          name="area"
          @blur="checkText($event, inputArea)"
        />
        <span class="error__message">{{inputArea.errorText}}</span>
      </div>
    </div>

    <div class="form__row">
      <label for="textarea" class="text--md">
        Description
        <span class="star">*</span>
      </label>
      <div
        class="input input__textarea"
        :class="{error:  inputDescription.isValid!==null && !inputDescription.isValid} "
      >
        <textarea
          name="textarea"
          class="input__field input__field--area req"
          :placeholder="inputDescription.placeholder"
          v-model="inputDescription.value"
          id="textarea"
          cols="30"
          rows="10"
          @blur="checkText($event, inputDescription)"
        ></textarea>
        <span class="error__message">{{inputDescription.errorText}}</span>
      </div>
    </div>

    <div class="form__row form__row--right">
      <inputFile @files="getFilesData" />
    </div>

    <div class="btn__wrapper">
      <input type="submit" class="btn btn__submit" value="Submit" />
    </div>
  </form>
</template>

<script>
import inputFile from "@/components/components/inputFile.vue";

export default {
  data: function() {
    return {
      numberIsValid: "This field in required",
      formValid: false,
      files: 0,
      inputUserName: {
        required: false,
        errorText: "This field in required",
        placeholder: "Type text",
        value: "",
        isValid: true
      },
      inputNumberOfPeople: {
        required: true,
        errorText: "This field in required",
        errorText2: "Please enter number from 1 to 99",
        placeholder: "1-99",
        value: "",
        isValid: null
      },
      inputArea: {
        required: true,
        errorText: "This field in required",
        placeholder: "Design, Marketing, Development, etc.",
        value: "",
        isValid: null
      },
      inputDescription: {
        required: true,
        errorText: "This field in required",
        placeholder: "Type text",
        value: "",
        isValid: null
      }
    };
  },
  components: {
    inputFile
  },
  methods: {
    checkNumber() {
      let num = this.inputNumberOfPeople.value;

      if (num == "" || num == null) {
        this.numberIsValid = this.inputNumberOfPeople.errorText;
        this.inputNumberOfPeople.isValid = false;
      } else if (num < 1 || num > 99) {
        this.numberIsValid = this.inputNumberOfPeople.errorText2;
        this.inputNumberOfPeople.isValid = false;
      } else {
        this.inputNumberOfPeople.isValid = true;
      }
    },
    checkText(e, obj) {
      return obj.value ? (obj.isValid = true) : (obj.isValid = false);
    },
    getFilesData(data) {
      this.files = data.nameOfFiles;
    },
    checkForm() {
      let inputs = [
        this.inputUserName,
        this.inputNumberOfPeople,
        this.inputArea,
        this.inputDescription
      ];

      let inputsValue = [];

      for (let i of inputs) {
        if (!i.isValid) {
          i.isValid = false;
        }
        inputsValue.push(i.isValid);
      }

      this.formValid = inputsValue.every(i => i === true);

      if (this.formValid) {
        console.group("Customer message");
        console.log(`Company name: ${this.inputUserName.value}`);
        console.log(`Number of people: ${this.inputNumberOfPeople.value}`);
        console.log(`Business area: ${this.inputArea.value}`);
        console.log(`Description: ${this.inputDescription.value}`);
        console.dir(`Files: ${this.files}`);
        console.groupEnd();
      }
    }
  }
};
</script>
