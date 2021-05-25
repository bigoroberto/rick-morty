<template>
  <div class="col-sm-6 col-md-4 col-lg-3">
      <h3>{{card.name}}</h3>
      <img class="img-fluid mb-3"
      :src="card.image"
      :alt="card.name">
      <h4>{{card.species}}</h4>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props:{
    card: Object
  }
}
</script>

<style lang="scss" scoped>
h3{
  min-height: 67px;
}
img{
  border-radius: 50%;
  box-shadow: 0 5px 5px rgba($color: black, $alpha: 0.5);
  transition: all .3s;
  &:hover{
    transform: scale(1.05, 1.05);
    filter: brightness(130%);
    box-shadow: 0 15px 15px rgba($color: black, $alpha: 0.5);
  }
}
</style>