<template>
  <form @submit.prevent="errors && $emit('toLastPage')">
    <div class="input-field">
      <label for="postal">Почтовый индекс</label>
      <input type="text" name="postal" id="postal" />
    </div>
    <div class="input-field">
      <label for="contry">Страна</label>
      <input type="text" name="contry" id="contry" />
    </div>
    <div class="input-field">
      <label for="oblast">Область</label>
      <input type="text" name="oblast" id="oblast" />
    </div>
    <div class="input-field">
      <label for="city">Город*</label>
      <div class="input">
        <span class="error" v-if="v$.city.$error"
          >Введите город проживания</span
        >
        <input
          :class="[v$.city.$error ? 'input-error' : '']"
          v-model.trim="city"
          type="text"
          name="city"
          id="city"
        />
      </div>
    </div>
    <div class="input-field">
      <label for="street">Улица</label>
      <input type="text" name="street" id="street" />
    </div>
    <div class="input-field">
      <label for="house">Дом</label>
      <input type="text" name="house" id="house" />
    </div>
    <div class="input-field">
      <label for="document">Тип документа*</label>
      <div class="input">
        <span class="error" v-if="v$.documentType.$error"
          >Выберите тип документа</span
        >
        <div class="custom-select">
          <select
            class="select"
            :id="[v$.documentType.$error ? 'custom-select-error' : '']"
            v-model="documentType"
            name="document"
          >
            <option value="">Выбрать</option>
            <option value="pasport">Паспорт</option>
            <option value="birthSert">Свидетельство о рождении</option>
            <option value="driverLicense">Водительское удовстоверение</option>
          </select>
        </div>
      </div>
    </div>
    <div class="input-field">
      <label for="serial">Серия</label>
      <input type="text" name="serial" id="serial" />
    </div>
    <div class="input-field">
      <label for="serialNumb">Номер</label>
      <input type="text" name="serialNumb" id="serialNumb" />
    </div>
    <div class="input-field">
      <label for="byWhom">Кем выдан</label>
      <textarea id="byWhom" class="textarea"></textarea>
    </div>
    <div class="input-field">
      <label for="issue">Дата выдачи*</label>
      <div class="input">
        <span class="error" v-if="v$.dateOfIssue.$error"
          >Неверная дата выдачи</span
        >
        <input
          :class="[v$.dateOfIssue.$error ? 'input-error' : '']"
          v-model="dateOfIssue"
          type="date"
          min="1900-01-01"
          max="2021-03-25"
          name="issue"
          id="issue"
        />
      </div>
    </div>
    <div class="input-field">
      <input
        @click="$emit('toFirstPage')"
        type="button"
        value="Назад"
        class="btn"
      />
    </div>
    <div class="input-field register">
      <input
        @click="submitForm"
        type="submit"
        value="Зарегистрироваться"
        class="btn"
      />
    </div>
  </form>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import {
  required,
  alpha,
} from "@vuelidate/validators";
export default {
  emits: ["toFirstPage", "toLastPage"],
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      city: "",
      documentType: "",
      dateOfIssue: "",
    };
  },
  computed: {
    errors() {
      return this.v$.$errors.length === 0;
    },
  },
  validations() {
    return {
      city: {
        required,
        checkCity(city) {
          const regex = /^[a-zA-ZА-Яа-я\s-]+$/;
          return regex.test(city);
        },
      },
      documentType: {
        required,
        alpha,
      },
      dateOfIssue: {
        required,
      },
    };
  },
  methods: {
    submitForm() {
      this.v$.$validate();
      if (!this.v$.$error) {
        // Обработка формы
      }
    },
  },
};
</script>
