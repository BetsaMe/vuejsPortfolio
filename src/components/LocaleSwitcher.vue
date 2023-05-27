<template>
  <div class="ctn-languages">
    <button
      @click="
        this.$i18n.locale = 'fr';
        toggle();
      "
      type="button"
      class="toggle-style"
      :class="{ activeclass: isActive }"
    >
      FR
    </button>
    <button
      @click="
        this.$i18n.locale = 'en';
        toggle();
      "
      type="button"
      class="toggle-style"
      :class="{ activeclass: !isActive }"
    >
      EN
    </button>
  </div>
</template>

<script>
export default {
  name: "LocaleSwitcher",
  data() {
    return {
      locales: ["en", "fr"],
      isActive: true,
    };
  },
  methods: {
    toggle() {
      this.isActive = !this.isActive;
    },
  },
};
</script>

<style>
.ctn-languages {
  display: flex;
  justify-content: center;
  width: 35%;
}
.ctn-languages button {
  background-color: transparent;
  border: none;
  width: 40px;
  cursor: pointer;
}
.activeclass {
  text-decoration: underline 1.5px var(--pink) wavy;
  font-weight: bold;
}
.toggle-style {
  color: var(--grey2)
}
@media only screen and (max-width: 768px) {
  .toggle-style {
    font-size: 16px;
    margin: 0 8px;
  }
}
</style>
