<template>
  <form @submit.prevent="errors && $emit('toSecondPage', firstName, lastName)">
    <div class="input-field">
      <label for="firstName">Имя*</label>
      <div class="input">
        <span class="error" v-if="v$.firstName.$error">Введите ваше имя</span>
        <input
          v-model.trim="firstName"
          :class="[v$.firstName.$error ? 'input-error' : '']"
          type="text"
          name="firstName"
          id="firstName"
        />
      </div>
    </div>

    <div class="input-field">
      <label for="lastName">Фамилия*</label>
      <div class="input">
        <span class="error" v-if="v$.lastName.$error"
          >Введите вашу фамилию</span
        >
        <input
          :class="[v$.lastName.$error ? 'input-error' : '']"
          v-model.trim="lastName"
          type="text"
          name="lastName"
          id="lastName"
        />
      </div>
    </div>
    <div class="input-field">
      <label for="patronymic">Отчество</label>
      <input type="text" name="patronymic" id="patronymic" />
    </div>
    <div class="input-field">
      <label for="dob">Дата рождения*</label>
      <div class="input">
        <span class="error" v-if="v$.dob.$error">Неверная дата рождения</span>
        <input
          :class="[v$.dob.$error ? 'input-error' : '']"
          v-model="dob"
          type="date"
          min="1900-01-01"
          max="2021-03-25"
          name="dob"
          id="dob"
        />
      </div>
    </div>
    <div class="input-field">
      <label for="gender">Пол</label>
      <div class="custom-select">
        <select class="select" name="gender" id="gender">
          <option value="">Выбрать</option>
          <option value="male">Мужской</option>
          <option value="female">Женский</option>
        </select>
      </div>
    </div>
    <div class="input-field">
      <label for="tel">Номер телефона*</label>
      <div class="input">
        <span class="error" v-if="v$.phoneNum.$error">11 цифр начиная с 7</span>
        <input
          placeholder="7"
          :class="[v$.phoneNum.$error ? 'input-error' : '']"
          v-model="phoneNum"
          type="text"
          id="tel"
        />
      </div>
    </div>

    <div class="input-field">
      <label for="client-group">Группа клиентов*</label>
      <div class="input">
        <span class="error" v-if="multiError">Выберите группы клиентов</span>
        <div class="custom-select">
          <select
            class="select"
            :id="[multiError ? 'multi-error' : '']"
            @change="userChoice"
            name="client-group"
          >
            <option value="">Выбрать</option>
            <option>VIP</option>
            <option>Проблемные</option>
            <option>ОМС</option>
          </select>
        </div>
      </div>
    </div>
    <div v-if="userChoicesNotEmpty" class="input-field">
      <label for="selected-groups">Выбранные группы</label>
      <div class="groups-container">
        <div
          @click="removeGroup(userChoice)"
          class="groups"
          v-for="userChoice in userChoices"
          :key="userChoice"
        >
          {{ userChoice }}
        </div>
      </div>
    </div>
    <div class="input-field">
      <label for="doctor">Лечащий врач</label>
      <div class="custom-select">
        <select class="select" name="doctor" id="doctor">
          <option value="">Выбрать</option>
          <option value="ivanov">Иванов</option>
          <option value="zaharov">Захаров</option>
          <option value="chernisheva">Чернышева</option>
        </select>
      </div>
    </div>
    <div class="input-field sms">
      <label class="check">
        <input id="sms" type="checkbox" />
        <span class="checkmark"></span>
      </label>
      <label for="sms">Не отправлять СМС</label>
    </div>
    <div class="input-field">
      <input
        @click="submitForm"
        type="submit"
        value="Ещё один шаг"
        class="btn"
      />
    </div>
  </form>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";
export default {
  emits: ["toSecondPage"],
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      firstName: "",
      userChoices: [],
      lastName: "",
      dob: "",
      phoneNum: "",
      multiError: false,
    };
  },
  validations() {
    return {
      firstName: {
        required,
        checkFirstName(firstName) {
          const regex = /^[a-zA-ZА-Яа-я]+$/;
          return regex.test(firstName);
        },
      },
      lastName: {
        required,
        checklastName(lastName) {
          const regex = /^[a-zA-ZА-Яа-я\s-]+$/;
          return regex.test(lastName);
        },
      },
      dob: {
        required,
      },
      phoneNum: {
        required,
        checkPhoneNum(phoneNum) {
          const regex = /7{1}[0-9]{10}/;
          return regex.test(phoneNum);
        },
      },
    };
  },
  computed: {
    userChoicesNotEmpty() {
      return this.userChoices.length > 0;
    },
    errors() {
      return this.v$.$errors.length === 0;
    },
  },
  methods: {
    toggleList() {
      this.listVisible = !this.listVisible;
    },
    userChoice(e) {
      if (!this.userChoices.includes(e.target.value) && e.target.value !== "") {
        this.userChoices.push(e.target.value);
        this.multiError = false;
      }
      e.target.value = "";
    },
    removeGroup(userChoice) {
      this.userChoices = this.userChoices.filter(
        (group) => userChoice !== group
      );
      if (this.userChoices.length === 0) {
        this.multiError = true;
      }
    },
    submitForm() {
      this.v$.$validate();
      if (this.userChoicesNotEmpty === false) {
        this.multiError = true;
      }
    },
  },
};
</script>