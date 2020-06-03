<template>
  <div class="home-page">
    <h1 class="title title--lg">Your first project</h1>
    <Stages />
    <div class="home-page__form">
      <Form />
    </div>
  </div>
</template>

<script>
import Form from "@/components/parts/Form";
import Stages from "@/components/parts/Stages";

export default {
  name: "Home",
  components: {
    Form,
    Stages
  }
};
</script>
