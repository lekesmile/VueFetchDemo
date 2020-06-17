<template>
  <div class="card">
  <!-- <img src= {{image}}  alt="Avatar" style="width:100%"> -->
  <div class="container">
    <h4><b> {{nameTitle}} </b></h4>
    <p> {{gid }} </p>
  </div>
</div>
</template>

<script>
export default {
  name: 'CardsTemp',
  props: {
    // image: String,
    nameTitle: String,
    gid: String
  }
}
</script>

<style>
.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 40%;
  margin: 5px;
  background-image: linear-gradient(to right, rgb(218, 218, 84), rgba(66, 235, 89, 0.815));
  color: white;
  align-content: center;
  justify-content: center;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container {
  padding: 2px 16px;
}
.container h4{
  text-transform: uppercase;
  color: rgb(39, 8, 99);
}

</style>