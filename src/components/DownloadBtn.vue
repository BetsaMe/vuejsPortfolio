<template>
  <div
    class="btn-arrow-dynamic"
    :style="buttonStyles"
    @mouseover="hover = true"
    @mouseleave="hover = false"
  >

    <span class="label" :style="labelStyles">{{ title }}</span>
    <img
      src="/images/whitearrow-01.svg"
      alt="arrow"
      class="icon-arrow after"
      :style="arrowHoverStyles"
    />
  </div>
</template>


<script>
export default {
  name: "CustomizableDownloadBtn",
  props: {
    title: {
      type: String,
      required: true,
    },
    bgColor: {
      type: String,
      default: "#616FE4",
    },
    textColor: {
      type: String,
      default: "#fff",
    },
    borderColor: {
      type: String,
      default: "transparent",
    },
    hoverBgColor: {
      type: String,
      default: "#4a5cc4",
    },
    hoverTextColor: {
      type: String,
      default: "#fff",
    },
    hoverBorderColor: {
      type: String,
      default: "transparent",
    },
  },
  data() {
    return {
      hover: false,
    };
  },
  computed: {
    buttonStyles() {
      return {
        backgroundColor: this.hover ? this.hoverBgColor : this.bgColor,
        color: this.hover ? this.hoverTextColor : this.textColor,
        border: `1px solid ${this.hover ? this.hoverBorderColor : this.borderColor}`,
      };
    },
    labelStyles() {
      return {
        transform: this.hover ? "translateX(0px)" : "translateX(14px)",
        transition: "transform 0.3s ease",
        display: "inline-block",
      };
    },
    arrowHoverStyles() {
      return {
        opacity: this.hover ? 1 : 0,
        transform: this.hover ? "translateX(0) scaleX(1)" : "translateX(75%) scaleX(0.1)",
        transition: "all 0.3s ease",
        height: "28px",
        width: "28px",
      };
    },
  },
};
</script>

<style>
.btn-arrow-dynamic {
    transition: all 0.3s ease;
    display: inline-flex;
    align-items: center;
    justify-content: center; 
    padding: 12px 28px;
    border-radius: 60px;
    text-transform: uppercase;
    cursor: pointer;
    font-size: 15px;
    font-weight: bold;
    line-height: 24px;
    font-family: "Montserrat", sans-serif;
    position: relative;
    overflow: hidden;   /* Ocultar contenido extra */
    white-space: nowrap; /* Evitar que el texto se envuelva */
    width: auto; /* Asegurar que el ancho sea automático */
}

@media only screen and (max-width: 480px){
  .btn-arrow-dynamic{
    padding: 10px 30px !important;
    font-size: 13px !important;
  }

}


</style>

