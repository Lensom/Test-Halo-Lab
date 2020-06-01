<template>
  <div class="form__wrapper">
    <form id="form" class="form" @submit="checkForm" action="#" method="post">
      <p>
        <label for="name">Имя</label>
        <input
          ref="textRef"
          id="name"
          v-model="name"
          type="text"
          name="name"
          required
          @blur="checkText"
        />
      </p>

      <p :class="{'error': ageIsValid}">
        <label for="age">Возраст</label>
        <input id="age" v-model="age" type="number" name="age" @blur="checkAge" required />
        <span v-if="ageIsValid">Поле заполено неверно</span>
      </p>

      <p>
        <label for="area">Имя</label>
        <input id="area" v-model="area" type="text" name="area" @blur="checkText" required />
      </p>

      <p>
        <label for="textarea">Текст</label>
        <textarea
          name="textarea"
          v-model="textarea"
          id="textarea"
          cols="30"
          rows="10"
          @blur="checkText"
        ></textarea>
      </p>

      <p>
        <input
          type="file"
          id="files"
          name="files"
          multiple
          accept="image/*, image/jpeg"
          @change="countingLoadFiles"
          ref="files"
        />
        <span>You are loading {{amountLoadFiles}}</span>
      </p>

      <p>
        <input type="submit" value="Отправить" />
      </p>
    </form>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      name: null,
      age: null,
      ageIsValid: false,
      area: null,
      textarea: null,
      amountLoadFiles: 0
    };
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
    countingLoadFiles() {
      this.amountLoadFiles = this.$refs.files.files.length;
    },
    checkForm() {}
  }
};
</script>
