<template>
  <div id="app">
    
    <div class="container">
      <div id="logo">
        <img src="./assets/check.png" alt="">
        <span id="logotype-check">Checklist</span>
      </div>
      <form @submit.prevent="addCheck(check)">
        <input type="text" name="" id="input-item" placeholder="Escreva um item..." v-model="check.title">
        <button type="submit" id="submit-button">CRIAR</button>
      </form>
      <!-- {{ checks }} -->
      <div id="no-checks" class="check-row" v-if="checks.length == 0">
        <img src="./assets/attention.svg">
        <h3>Adicione um item para a checklist.</h3>
      </div>
      <div v-for="(c, index) in checks" :key="c.id" class="checklist check-column">
          <hr v-if="index > 0">
          <div class="check-item check-row">
            <div class="check-infos check-row">
              <input type="checkbox" name="" class="checkbox" v-model="c.checked">
              <div class="check-text">
                <h2 v-if="!c.checked" class="check-title">{{ c.title }}</h2>
                <h2 v-else class="checked-title">{{ c.title }}</h2>
              </div>
            </div>
            <div class="button-area">
              <a @click="removeCheck(index)" href="#"><img class="trash-icon" src="./assets/trash.svg"></a>
            </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return { checks: [], check: { checked: false } }
  },
  methods: {
    addCheck(check) {
      check.id = Date.now();
      this.checks.push(check);
      this.check = { checked: false };
    },

    removeCheck(index) {
      this.checks.splice(index, 1)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Source Sans Pro', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Source Sans Pro', sans-serif;
}

.container {
  width: 100%;
  height: 100vh;
  background-color: #f2f2f2;
  padding-top: 60px;
}

#logo {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 30px;

  font-size: 40px;
  font-style: italic;
  font-weight: bolder;
  font-family: Consolas;
}

#logo > img {
  height: 50px;
}

#logotype-check {
    margin-left: 10px;
}

#no-checks img {
  height: 25px;
  margin-right: 15px;
}

#no-checks h3 {
  color: #555;
  font-style: italic;
}

form {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: row;

  margin-bottom: 50px;
}

#input-item {
  height: 40px;
  width: 250px;
  margin-right: 10px;
  padding-left: 13px;
  color: #333;
  font-size: 12pt;

  border: none;
  border-radius: 15px;
  outline: none;
  box-shadow: 0 7px 10px #00000010;
}

#input-item::placeholder {
  color: #888;
  font-size: 10pt;
  font-style: italic;
}

#input-item:focus {
  border: 1px solid #4488dd;
}

#submit-button {
  width: 90px;
  height: 40px;
  
  border-radius: 15px;
  border: none;
  box-shadow: 0 7px 10px #00000010;

  color: #fff;
  font-weight: bolder;
  font-family: 'Source Sans Pro', sans-serif;
  font-size: 12pt;

  background: #44dd88;
  transition: 300ms;
}

#submit-button:hover {
  background: #32c760;
}

/* --> check */
.check-column {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.check-row {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.checklist {
  
}

.check-item {
  margin: 0;
}

.checkbox {
  height: 20px;
  width: 20px;
  margin-right: 15px;
}

.check-text {
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: start;
  text-align: left;
}

.check-text > input {
  border: none;
  outline: none;
  background: transparent;
}

.check-title {
  width: 400px;
  font-size: 20px;
  font-weight: bolder;
  color: #333;
}

.checked-title {
  width: 400px;
  font-size: 20px;
  font-weight: 400;
  text-decoration: line-through;
  color: #888;
}

.check-description {
  width: 400px;
  font-size: 12pt;
  color: #555;
}

img.trash-icon {
  height: 25px;
  color: #cc5566;
  margin-left: 15px;
}

hr {
  border: none;
  border-top: 1px solid #ccc;
  width: 500px;
  margin: 15px 0;
}
</style>
