<template>
  <div class="ctn-languages">   
      <select aria-label="language selection" v-model="$i18n.locale" class="language-select">
        <option value="es">ES</option>
        <option value="en">EN</option>
        <option value="fr">FR</option>
      </select>
  </div>
</template>

<script>
export default {
  name: "LocaleSwitcher",
  data() {
    return {
      locales: ["es","en", "fr"]
    };
  }
};
</script>

<style>
.ctn-languages {
  display: flex;
  justify-content: center;
  width: 35%;
}
select {
  border: 0;
  outline: 0;
  background: none;
  color: inherit;
  box-shadow: none;
  cursor: pointer;
  padding: 0.8em;
  font-size: 15px;
}
.language-select {
  text-decoration: underline 1.2px var(--pink);
}

@media only screen and (max-width: 768px) {
  .toggle-style {
    font-size: 16px;
    margin: 0 8px;
  }
}
</style>
