<template>
  <div class="ctn-languages" >
    <select
      aria-label="language selection"
      v-model="$i18n.locale"
      @blur="closeDropdown"
    >
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
      locales: ["es", "en", "fr"],
    };
  },
};
</script>

<style>
.ctn-languages {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  box-shadow: none;
  border-radius: 0;
}

select {
  border: 0;
  outline: 0;
  background: none;
  font-weight: 500;
  box-shadow: none;
  cursor: pointer;
  font-size: 15px;
  padding: 10px;
}
select::-ms-expand {
  display: none; /* Quitar el icono predeterminado en IE y Edge */
}

select:focus {
  outline: none; /* Quitar el contorno al hacer foco */
  box-shadow: none; /* Asegurarse de que no hay sombra en focus */
}

@media only screen and (max-width: 768px) {
  .toggle-style {
    font-size: 16px;
    margin: 0 8px;
  }
}
</style>
