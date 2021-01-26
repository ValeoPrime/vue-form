<template>
  <div class="form__wrapper">
    <form class="register__form">
      <h2 class="form__title">Регистрация</h2>
      <div class="form__descr">
        Уже есть аккаунт?&nbsp;
        <span>
          <a href="/#">Войти</a>
        </span>
      </div>

      <Input
        v-for="input of inputs"
        :input="input"
        :key="input.id"
        @inputChange="inputHandler"
      />

      <DropDown @languageHandler="languageHandler" :langArr="langArr" />

      <div class="therms__use">
        <input
          class="therms__use__input"
          type="checkbox"
          id="thermsUse"
          @change="thermsUseHandler"
          :checked="thermsUse"
        />
        <label htmlFor="thermsUse">
          Принимаю &nbsp;
          <span>
            <a href="/#">условия</a>
          </span>
          &nbsp; использования
        </label>
      </div>

      <button class="submit__button" type="submit" :disabled="submitDenied">
        Зарегистрироваться
      </button>
    </form>
  </div>
</template>

<script>
import Input from "./components/Input.vue";
import DropDown from "./components/DropDown.vue";

function inputValidate(value, regExp) {
  var regexp = new RegExp(regExp);
  var matches = value.match(regexp);
  return matches == null ? false : true;
}

export default {
  name: "App",
  data() {
    return {
      inputs: [
        {
          name: "Имя",
          placeholder: "Введите Ваше имя",
          id: "name",
          errorText: "",
        },
        {
          name: "Email",
          placeholder: "Введите Ваш Email",
          id: "email",
          errorText: null,
        },
        {
          name: "Номер телефона",
          placeholder: "Введите Ваш номер телефона",
          id: "tel",
          errorText: null,
        },
      ],
      registerData: {
        name: "",
        tel: "",
        email: "",
        lang: "",
        thermsUse: false,
      },
      langArr: [
        {
          id: "rus",
          title: "Русский",
        },
        {
          id: "eng",
          title: "Английский",
        },
        {
          id: "chi",
          title: "Китайский",
        },
        {
          id: "spa",
          title: "Испанский",
        },
      ],
      validateRulls: {
        name: {
          errorMessage: "Допустимы буквы, пробел, дефис",
          validateExp: "^[A-Za-zА-яа-я -]+$",
        },
        email: {
          errorMessage: "Введите корректный Емаил",
          validateExp: "^.+@.+\\..+$",
        },
        tel: {
          errorMessage: "Допустимо макс 11 цифр, тире, плюс, скобки",
          validateExp: "^[0-9()-+]+$",
        },
      },
      thermsUse: false,
    };
  },
  methods: {
    languageHandler(id) {
      id ? (this.registerData.lang = id) : null;
    },
    inputHandler(value, id) {
      if (inputValidate(value, this.validateRulls[id].validateExp)) {
        this.inputs = this.inputs.map((input) => {
          input.errorText = "";
          return input;
        });
        if (value.trim().length > 3) {
          this.registerData[id] = value;
        }
      } else {
        this.inputs = this.inputs.map((input) => {
          if (input.id === id) {
            input.errorText = this.validateRulls[id].errorMessage;
          }
          return input;
        });
      }
    },
    thermsUseHandler() {
      this.thermsUse = !this.thermsUse;
      this.registerData.thermsUse = this.thermsUse;
    },
  },
  computed: {
    submitDenied() {
      return (
        !this.registerData.name ||
        !this.registerData.tel ||
        !this.registerData.email ||
        !this.registerData.lang ||
        !this.registerData.thermsUse
      );
    },
  },
  components: {
    Input,
    DropDown,
  },
};
</script>

<style scoped>
.form__wrapper {
  margin: 0 auto;
  max-width: 460px;
  min-width: 360px;
  background: #ffffff;
  box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.02),
    0px 32px 64px rgba(44, 39, 56, 0.04);
  border-radius: 24px;
  padding: 40px 30px;
  box-sizing: border-box;
}

.register__form {
  color: #2c2738;
  max-width: 100%;
}

.form__title {
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 34px;
  line-height: 44px;
}

.form__descr {
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 22px;
  margin-bottom: 56px;
}

span a {
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 22px;
  color: #0880ae;
  text-decoration: none;
}

.therms__use {
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 21px;
  color: #756f86;
  margin-bottom: 37px;
  display: flex;
  align-items: center;
}

.therms__use__input {
  position: absolute;
  z-index: -1;
  opacity: 0;
}

.therms__use__input + label {
  display: inline-flex;
  align-items: center;
  user-select: none;
}

.therms__use__input + label::before {
  content: "";
  display: inline-block;
  width: 28px;
  height: 28px;
  flex-shrink: 0;
  flex-grow: 0;
  background: #ffffff;
  border: 1px solid #dbe2ea;
  box-sizing: border-box;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
  border-radius: 4px;
  margin-right: 8px;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 50% 50%;
}

.therms__use__input:checked + label::before {
  background-image: url("~@/assets/Mask.svg");
  border: 2px solid #0880ae;
}

.submit__button {
  font-family: IBM Plex Sans, sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 21px;
  text-align: center;
  color: #ebf4f8;
  background: #0880ae;
  padding: 17.5px 0;
  width: 100%;
  box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
    0px 4px 8px rgba(44, 39, 56, 0.08);
  border-radius: 6px;
  border: none;
  outline: none;
  cursor: pointer;
}

.submit__button:disabled {
  background: #dbe2ea;
  color: #b1b5bf;
}

@media screen and (max-width: 600px) {
  .form__wrapper {
    padding: 20px 15px;
  }
  .form__descr {
    margin-bottom: 25px;
  }
}
</style>
