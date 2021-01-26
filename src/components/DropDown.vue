<template>
  <div class="dropDown__wrap">
    <button
      class="dropDown__button"
      :class="{ open: dropDownShow }"
      type="button"
      @click="dropDownHandler"
    >
      {{ dropDownText }}
    </button>
    <ul class="dropDown__body" :class="{ show: dropDownShow }">
      <li
        v-for="lang in langArr"
        @click="dropDownHandler($event.target)"
        :id="lang.id"
        :key="lang.id"
      >
        {{ lang.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["langArr"],
  data() {
    return {
      dropDownShow: false,
      dropDownText: "язык",
    };
  },
  methods: {
    dropDownHandler(target) {
      this.dropDownShow = !this.dropDownShow;
      target.innerText
        ? (this.dropDownText = target.innerText)
        : (this.dropDownText = "язык");
      target.innerText
        ? this.$emit("languageHandler", target.id ? target.id : null)
        : null;
    },
  },
};
</script>

<style scoped>
.dropDown__wrap {
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 21px;
  color: #756f86;
  position: relative;
}

.dropDown__button {
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 21px;
  color: #7c9cbf;
  background: #ffffff;
  border: 1px solid #dbe2ea;
  box-sizing: border-box;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
  border-radius: 6px;
  padding: 16px 57px 16px 16px;
  width: 100%;
  margin-top: 7px;
  margin-bottom: 37px;
  outline: none;
  text-align: left;
  position: relative;
  cursor: pointer;
}

.dropDown__button::before {
  content: "";
  position: absolute;
  right: 11px;
  top: calc(50% - 15px);
  width: 30px;
  height: 30px;
  background-position: center center;
  background-repeat: no-repeat;
  background-image: url("~@/assets/arrow__bottom.svg");
}

.dropDown__body {
  background: #ffffff;
  box-sizing: border-box;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04),
    0px 20px 20px rgba(44, 39, 56, 0.04);
  border-radius: 6px;
  position: absolute;
  width: 100%;
  top: 65px;
  animation: all 1s;
  overflow: hidden;
  height: 0;
}

.dropDown__body li {
  padding: 12px 15px;
  cursor: pointer;
}

.dropDown__body li:hover {
  background: #ebf4f8;
}

.open {
  border: 2px solid #0880ae;
}

.show {
  padding: 12px 0;
  border: 1px solid #dbe2ea;
  height: 200px;
}
</style>
