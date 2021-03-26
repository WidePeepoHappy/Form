<template>
  <div class="form-container">
    <div class="title">
      <h2>Форма регистрации</h2>
    </div>
    <first-page
      @toSecondPage="toSecondPage"
      v-show="showFirstPage"
    ></first-page>
    <second-page
      @toFirstPage="toFirstPage"
      @toLastPage="toLastPage"
      v-show="showSecondPage"
    ></second-page>
    <registration-confirmation
      v-show="showLastPage"
      :firstName="userFirstName"
      :lastName="userLastName"
    ></registration-confirmation>
  </div>
</template>

<script>
import FirstPage from "./components/FirstPage";
import SecondPage from "./components/SecondPage";
import RegistrationConfirmation from "./components/RegistrationConfirmation";
export default {
  components: {
    FirstPage,
    SecondPage,
    RegistrationConfirmation,
  },
  name: "App",
  data() {
    return {
      showFirstPage: true,
      showSecondPage: false,
      showLastPage: false,
      userFirstName: "",
      userLastName: "",
    };
  },
  methods: {
    toSecondPage(firstName, lastName) {
      this.showFirstPage = false;
      this.showSecondPage = true;
      this.userFirstName = firstName;
      this.userLastName = lastName;
    },
    toFirstPage() {
      this.showFirstPage = true;
      this.showSecondPage = false;
    },
    toLastPage() {
      this.showLastPage = true;
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700&display=swap");

$primaryColor: #049bff;
$secondaryColor: #ff9b04;
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}
body {
  background-color: $primaryColor;
}
.form-container {
  max-width: 500px;
  width: 100%;
  background-color: #fff;
  margin: 50px auto;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 30px;
  .title {
    margin-bottom: 25px;
    color: $primaryColor;
    text-transform: uppercase;
    text-align: center;
    border-bottom: 3px solid $primaryColor;
  }
  form {
    width: 100%;
    .input-field {
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      label {
        width: 200px;
        color: #757575;
        margin-right: 5px;
        font-size: 14px;
      }
      .input {
        text-align: center;
        width: 100%;
        .error {
          text-align: center;
          color: $secondaryColor;
          font-size: 15px;
        }
      }
      input,
      textarea {
        width: 100%;
        outline: none;
        border: 1px solid #d5dbd9;
        font-size: 15px;
        padding: 8px 10px;
        border-radius: 3px;
        transition: all 0.3s ease;
      }
      textarea {
        width: 100%;
        height: 125px;
        resize: none;
      }
      input:focus,
      textarea:focus,
      .custom-select select:focus {
        border-color: $primaryColor;
      }
      .groups-container {
        width: 100%;
        .groups {
          display: inline-block;
          margin: 0 10px;
          padding: 6px 12px;
          background-color: #eee;
          border-radius: 3px;
          font-size: 14px;
          font-weight: bold;
          color: $primaryColor;
          cursor: pointer;
        }
      }
      .custom-select {
        position: relative;
        width: 100%;
        height: 38px;
        margin-left: -1px;
        .select {
          -webkit-appearance: none;
          -moz-appearance: none;
          appearance: none;
          outline: none;
          width: 100%;
          height: 100%;
          padding: 8px 10px;
          font-size: 15px;
          border: 1px solid #d5dbd9;
          border-radius: 3px;
        }
        #multi-error {
          border: 1px solid $secondaryColor;
        }
        #custom-select-error {
          border: 1px solid $secondaryColor;
        }
      }
      .custom-select::before {
        content: "";
        position: absolute;
        top: 12px;
        right: 10px;
        border: 8px solid;
        border-color: #d5dbd9 transparent transparent transparent;
        pointer-events: none;
      }
      .input-error {
        border: 1px solid $secondaryColor;
      }
      .check {
        width: 15px;
        height: 15px;
        position: relative;
        display: block;
        cursor: pointer;
        input {
          display: none;
        }
        input:checked ~ .checkmark {
          background-color: $primaryColor;
        }
        input:checked ~ .checkmark::before {
          display: block;
        }
        .checkmark {
          @extend .check;
          border: 1px solid $primaryColor;
        }
        .checkmark::before {
          content: "";
          position: absolute;
          top: 1px;
          left: 2px;
          width: 5px;
          height: 2px;
          border: 2px solid;
          border-color: transparent transparent #fff #fff;
          transform: rotate(-45deg);
          display: none;
        }
      }
      .btn {
        width: 100%;
        padding: 8px 10px;
        font-size: 15px;
        background-color: $primaryColor;
        color: #fff;
        cursor: pointer;
        border-radius: 3px;
        outline: none;
      }
      .btn:hover {
        opacity: 0.9;
      }
      .input-field:last-child {
        margin-bottom: 0;
      }
    }
    .register {
      .btn {
        background-color: $secondaryColor;
      }
      .btn:focus {
        border: 1px solid $secondaryColor;
      }
    }
  }
}
@media (max-width: 420px) {
  .form-container {
    form {
      .input-field {
        flex-direction: column;
        align-items: flex-start;
        label {
          margin-bottom: 5px;
        }
        .input {
          .error {
            margin: 0;
          }
        }
      }
      .sms {
        flex-direction: row;
      }
    }
  }
}
</style>

