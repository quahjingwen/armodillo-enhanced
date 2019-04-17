<template>
<div>
  <div class="choose">
    <button class ="test" @click="goReco" id="close-image">Help me Choose my Modules!<img src="../assets/selection.png" height= "200px" ></button>
  </div>
  <div class="choose2">
    <button class="test" @click = "goList" id="close-image">Let me choose my modules!<img src="../assets/choices.png" height= "200px" ></button>
  </div>
  </div>
</template>

<script>
export default {
  name: "choose",
  data() {
    return {};
  },
  methods: {
    goReco: function(){
      this.$router.push({ name: "Recommendation" });
    },
    goList: function(){
      this.$router.push({ name: "Choices" });
    }
  }
};
</script>

<style scoped>

.buttons{
  margin:20px;
  padding: 20px;
}

.choose{
  display:inline-block;
  margin: 30px;
  padding: 5px;
}
.choose2{
  display: inline-block;
  margin: 30px;

  padding: 5px;
}

.test{
background-color:rgb(253, 98, 27);
border: #2e6da4;
font-family: Arial, Geneva, Arial, Helvetica,  sans-serif;
font-size: 20px;
color: #fff;
letter-spacing: 1px;
padding: 8px 12px;
font-size: 20px;
font-weight: normal;
border-radius: 4px;
line-height: 1.5;
text-decoration:none
}
</style>