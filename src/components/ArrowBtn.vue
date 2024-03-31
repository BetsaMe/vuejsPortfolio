<template>
  <a
    class="btn-arrow underlined-02 "
  >
    <img src="/images/arrow-left.svg" alt="arrow" :class="{ 'before-arrow': arrowPosition === 'after' }"/>
    <span>{{title}}</span>
    <img src="/images/arrow-right.svg" alt="arrow" :class="{ 'after-arrow': arrowPosition === 'before' }"/>
  </a>
</template>

<script>
export default {
  name: "ArrowBtn",
  props:{
    title:{ type:String},
    arrowPosition: { type: String, default: 'after' } // Prop para la posición de la flecha, por defecto 'after'

  }
};
</script>

<style>
.btn-arrow {
  display: flex;
  align-items: center;
  width: fit-content;
}
.btn-arrow span {
  text-transform: uppercase;
  font-size: 14px;
  font-weight: 600;
  margin:0 8px;
}
.btn-arrow img {
  height: 30px;
  width: 30px;
}
.btn-arrow:hover {
  background-size: 100% 2px;
}
.before-arrow, .after-arrow{
  display: none;
}
@media screen and (max-width: 480px){
  .btn-arrow span {
    font-size: 12px;
  }
}


</style>

