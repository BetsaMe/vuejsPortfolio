<template>
  <div id="error">
    <div class="error-text">
      <h3 class="error-title">¡Sorry!</h3>
      <p>
        I looked everywhere for this page, <br />
        Are you sure the website URL is correct?
      </p>
      <a class="underlined-02" href="/">Back to home</a>
    </div>
    <div class="error-img">
      <img src="/images/errorpage.webp" alt="error" />
    </div>
  </div>
</template>

<script>
export default {
  name: "ErrorPage",
};
</script>

<style>

#error {
  display: flex;
  width: 100%;
  padding: 120px 20%;
  height: 100vh;
  align-items: center;
  justify-content: center;
}
.error-text {
  width: 50%;
  z-index: 30;
}
.error-title {
  font-family: "Literata", serif;
  font-size: 120px;
  font-weight: 100;
  margin: 0;
}
.error-text p {
  margin-bottom: 40px;
  line-height: 30px;
}
.error-img {
  width: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}
#error img {
  height: 380px;
}
#error a {
  font-weight: bold;
  cursor: pointer;
  text-transform: uppercase;
}
@media only screen and (max-width: 768px) {
  #error {
    flex-direction: column;
  }
  .error-title {
    font-size: 90px;
  }
  .error-text,
  .error-img {
    text-align: center;
    width: 100%;
  }
}
@media only screen and (max-width: 480px) {
  #error {
    padding: 20px;
  }
  .error-title {
    font-size: 60px;
  }
  .error-text {
    margin: 0;
  }
  #error img {
    height: 250px;
  }
}
</style>
