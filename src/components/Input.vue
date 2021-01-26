<template>
  <label className="text__input">
    {{ input.name }}
    <input
      type="text"
      @input="$emit('inputChange', $event.target.value, $event.target.id)"
      :placeholder="input.placeholder"
      :id="input.id"
      required="true"
    />

    <span className="error__message">{{ input.errorText }}</span>
  </label>
</template>

<script>
export default {
  props: ["input"],
};
</script>

<style scoped>
.text__input {
  display: flex;
  flex-direction: column;
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 21px;
  color: #756f86;
  margin-bottom: 34px;
  position: relative;
}

.text__input input {
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 21px;
  padding: 16px;
  margin-top: 6px;
  background: #ffffff;
  border: 1px solid #dbe2ea;
  box-sizing: border-box;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
  border-radius: 6px;
  color: #7c9cbf;
  outline: none;
}

.text__input input:focus {
  border: 2px solid #0880ae;
}

.error__message {
  position: absolute;
  bottom: -25px;
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 18px;
  color: #ff7171;
}
</style>
