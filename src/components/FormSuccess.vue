<template>
  <div class="form-success">
    <div class="form-success__text">
      <span>
        &#10003; <br />
        <span style="font-size: 18px">Форма отправлена</span></span
      >
    </div>
  </div>
</template>
<style scoped>
.form-success {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 300px;
  height: 300px;
  font-size: 55px;
  color: greenyellow;
  border-radius: 50%;
  border: 2px solid greenyellow;
  margin-left: auto;
  margin-right: auto;
}

.form-success__text > span {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
