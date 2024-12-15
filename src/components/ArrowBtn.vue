<template>
  <a
    :href="href"
    :target="target"
    class="btn-arrow"
  >    
    <span>{{ $t(title) }}</span>
    <img src="/images/arrow-right.svg" alt="arrow" class="after"/>
  </a>
</template>

<script>
export default {
  name: "ArrowBtn",
  props:{
    title:{ type:String},
    href:{ type:String},
    target:{ type:String},
  }
};
</script>

<style>
.btn-arrow {
  display: flex;
  align-items: center;
  width: fit-content;
  margin: 0 7.5px;
}
.btn-arrow span {
  font-size: 14px;
  line-height: 28px;
  font-weight: 600;
  text-transform: uppercase;
  text-decoration: underline;
}
.btn-arrow img {
  height: 30px;
  width: 30px;
  transition: transform 0.3s ease; /* Para animar el movimiento */  
}
.btn-arrow:hover {
  background-size: 100% 2px;
}

.btn-arrow span:hover ~ img {
  transform: rotate(-30deg); /* Cambia de "translate" a "transform" */
}

.btn-arrow span:hover{
  color: #616fe4;
} 
@media screen and (max-width: 480px){
  .btn-arrow span {
    font-size: 12px;
  }
}

</style>

