<template>
  <div>
    <div class="backdrop"></div>
    <dialog class="form-container" open>
      <header>
        <h1>Регистрация завершена</h1>
      </header>
      <div id="main">
        <section>
          <p>Добро пожаловать, {{ firstName }} {{ lastName }}</p>
        </section>
        <menu>
          <input
            @click.prevent="toHomePage"
            type="button"
            value="На домашнюю"
            id="btn"
          />
        </menu>
      </div>
    </dialog>
  </div>
</template>

<script>
export default {
  props: ["firstName", "lastName"],
};
</script>

<style scoped>
.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 10;
}

dialog {
  position: fixed;
  top: 30%;
  max-width: 500px;
  z-index: 100;
  border: none;
  padding: 20px;
  background-color: white;
}
section {
  text-align: center;
}
header {
  text-align: center;
  color: #049bff;
  width: 100%;
}
#btn {
  width: 100%;
  padding: 8px 10px;
  font-size: 15px;
  background-color: #ff9b04;
  color: #fff;
  cursor: pointer;
  border-radius: 3px;
  outline: none;
  border: none;
}
#btn:hover {
  opacity: 0.9;
}
#main {
  border-top: 3px solid #049bff;
}
p {
  padding: 20px;
}
</style>