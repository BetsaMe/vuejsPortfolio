<template>
  <a
    href="images/CV-Betsa-2022.pdf"
    download="CV-Betsa-2022"
    class="btn-download"
  >
    <img src="/images/arrow-01.svg" alt="arrow" class="icon-arrow before" />
    <span class="label">download cv</span>
    <img src="/images/whitearrow-01.svg" alt="arrow" class="icon-arrow after" />
  </a>
</template>

<script>
export default {
  name: "DownloadBtn",
};
</script>

<style scoped>
.btn-download {
  display: inline-block;
  font-size: 15px;
  line-height: 24px;
  width: 250px;
  min-width: 250px;
  padding: 12px 32px 12px 82px;
  position: relative;
  background-color: var(--white-bg);
  border: solid var(--black) 1px;
  font-family: "Montserrat", sans-serif;
  font-weight: bold;
  color: var(--grey1);
  text-transform: uppercase;
  cursor: pointer;
  transition: all 0.6s cubic-bezier(0.23, 1, 0.32, 1),
    color 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}
.btn-download .label {
  display: inline-block;
  transition: transform 0.5s cubic-bezier(0.86, 0, 0.07, 1);
}
.icon-arrow {
  fill: var(--grey1);
  height: 35px;
  width: 35px;
  transition: all 0.5s cubic-bezier(0.86, 0, 0.07, 1),
    opacity 0.4s cubic-bezier(0.86, 0, 0.07, 1);
}
.icon-arrow.before {
  position: absolute;
  left: 32px;
  top: 6px;
  margin-right: 15px;
  transform-origin: left center;
}
.icon-arrow.after {
  top: 6px;
  opacity: 0;
  position: absolute;
  right: 32px;
  transform: translateX(75%) scaleX(0.1);
  transform-origin: right center;
}
.btn-download:hover .label {
  transform: translateX(-40px);
}
.btn-download:hover .icon-arrow.before {
  opacity: 0;
  transform: translateX(-75%) scaleX(0.1);
}
.btn-download:hover .icon-arrow.after {
  opacity: 1;
  transform: translateX(0) scaleX(1);
}
.btn-download:hover,
.btn-download:focus {
  background: var(--black);
  color: var(--white-bg);
}

@media screen and (max-width: 1024px) {
  .btn-download {
    min-width: 250px;
  }
}
@media only screen and (max-width: 768px) {
  .btn-download {
    margin: 20px 0;
  }
}
</style>

