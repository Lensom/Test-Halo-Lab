<template>
  <div class="home-page">
    Home page
    <Stages />
    <Form />
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
