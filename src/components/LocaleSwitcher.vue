<template>
  <div class="ctn-languages" @click="toggleDropdown">
    <select
      aria-label="language selection"
      v-model="$i18n.locale"
      @blur="closeDropdown"
    >
      <option value="es">ES</option>
      <option value="en">EN</option>
      <option value="fr">FR</option>
    </select>
    <img src="/images/flecha_abajo.png" alt="flecha" class="down-arrow" :class="{ rotated: isOpen }" />
  </div>
</template>

<script>
export default {
  name: "LocaleSwitcher",
  data() {
    return {
      locales: ["es", "en", "fr"],
      isOpen: false, // Estado para controlar la animación de la flecha
    };
  },
  methods: {
    toggleDropdown() {
      this.isOpen = !this.isOpen;
    },
    closeDropdown() {
      this.isOpen = false;
    },
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

}

select {
  appearance: none; /* Ocultar la flecha predeterminada */
  -webkit-appearance: none;
  -moz-appearance: none;
  border: 0;
  outline: 0;
  background: none;
  color: var(--grey2);
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

.down-arrow {
  height: 24px;
  transition: transform 0.2s ease-in-out;
}

.down-arrow.rotated {
  transform: rotate(180deg);
}

@media only screen and (max-width: 768px) {
  .toggle-style {
    font-size: 16px;
    margin: 0 8px;
  }
}
</style>
