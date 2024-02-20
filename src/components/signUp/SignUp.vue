<script>
export default {
  data() {
    return {
      about: {
        name: "",
        surname: "",
        partonymic: "",
        birthDay: "",
        phone: "",
        sex: "male",
        clientGroup: [],
        doctor: "-",
        agreeGetMessages: true,
      },
      address: {
        index: "",
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
      },
      passport: {
        type: "*",
        seria: "",
        number: "",
        whoIssued: "",
        whenIssued: "",
      },

      clientGroups: [
        {
          label: "VIP",
          value: "VIP",
        },
        {
          label: "Проблемные",
          value: "Problems",
        },
        {
          label: "ОМС",
          value: "OMS",
        },
      ],
      doctors: [
        {
          label: "Захарова",
          value: "Zakharova",
        },
        {
          label: "Иванова",
          value: "Ivanova",
        },
        {
          label: "Чернышева",
          value: "Chernishova",
        },
      ],
      docTypes: [
        {
          label: "Паспорт",
          value: "passport",
        },
        {
          label: "Свидетельство о рождении",
          value: "birth certificate",
        },
        {
          label: "Вод. удостоверение",
          value: "driver's license",
        },
      ],
    };
  },
  methods: {
    clearOldErrors(fields) {
      fields.forEach((field) => {
        field.classList.remove("error-field");
      });
    },
    validationEmptyFields(fields) {
      let isThereEmptyFields = false;
      fields.forEach((field) => {
        if (!field.value || field.value == "*") {
          field.classList.add("error-field");
          isThereEmptyFields = true;
        }
      });
      if (isThereEmptyFields) {
        alert("Заполните обязательные поля!");
        return false;
      } else {
        return true;
      }
    },
    validationPhoneNumber(phone) {
      const phoneNumberNode = document.getElementById("phoneNumber");
      let noError = true;
      if (phone[0] == "+") {
        phone = phone.slice(1);
      }
      if (phone[0] != 7) {
        noError = false;
      }
      if (phone.length != 11) {
        noError = false;
      }
      if (!noError) {
        phoneNumberNode.classList.add("error-field");
        alert(
          "Некорректный номер телефона. Попробуйте еще раз. Номер должен начинаться с цифры 7 и иметь 11 символов!"
        );
        phoneNumberNode.value = "";
      }
      return noError;
    },
    onSubmit(event) {
      event.preventDefault();
      const requiredFieldsNodes = document.querySelectorAll(".required");

      this.clearOldErrors(requiredFieldsNodes);

      if (!this.validationEmptyFields(requiredFieldsNodes)) {
        return;
      }
      if (!this.validationPhoneNumber(this.about.phone)) {
        return;
      }
      alert("Вы успешно прошли регистрацию! Добро пожаловать!");
    },
  },
};
</script>
<template>
  <form class="form" @submit="onSubmit">
    <div class="bio">
      <input
        id="name"
        class="input required"
        v-model.trim="about.name"
        placeholder="Имя *"
        type="text"
      />
      <input
        id="surname"
        class="input required"
        v-model.trim="about.surname"
        placeholder="Фамилия *"
        type="text"
      />
      <input
        class="input"
        v-model.trim="about.partonymic"
        placeholder="Отчество"
        type="text"
      />
      <input
        class="input required"
        v-model.trim="about.birthDay"
        placeholder="Дата рождения *"
        type=""
      />
      <input
        id="phoneNumber"
        class="input required"
        v-model.trim="about.phone"
        placeholder="Номер телефона *"
        type="tel"
      />
      <div class="sex">
        <label>
          Мужчина
          <input v-model="about.sex" name="sex" type="radio" value="male" />
        </label>
        <label>
          Женщина
          <input v-model="about.sex" name="sex" type="radio" value="female" />
        </label>
      </div>
      <div class="group">
        <h3>Выберите группу клиента *</h3>
        <select
          class="client-group required"
          v-model="about.clientGroup"
          multiple
        >
          <option
            v-for="(group, index) in clientGroups"
            :key="index"
            :value="group.value"
          >
            {{ group.label }}
          </option>
        </select>
      </div>
      <div class="doctor">
        <h3 class="doctor__title">Выберите специалиста:</h3>
        <select class="doctor__selector" v-model="about.doctor">
          <option value="-" disabled>-</option>
          <option
            v-for="(doctor, index) in doctors"
            :key="index"
            :value="doctor.value"
          >
            {{ doctor.label }}
          </option>
        </select>
      </div>
      <div class="checkbox">
        <input
          type="checkbox"
          v-model="about.agreeGetMessages"
          class="checkbox__input"
          id="checkbox"
        />
        <label for="checkbox" class="checkbox__label"
          >Желаете получать СМС уведомления?</label
        >
      </div>
    </div>
    <div class="address">
      <h2 class="address__title">Адресс</h2>
      <div class="address__inputs">
        <input
          v-model="address.index"
          type="text"
          placeholder="Индекс"
          class="input"
        />
        <input
          v-model="address.country"
          type="text"
          placeholder="Страна"
          class="input"
        />
        <input
          v-model="address.region"
          type="text"
          placeholder="Область"
          class="input"
        />
        <input
          v-model="address.city"
          type="text"
          placeholder="Город *"
          class="input required"
        />
        <input
          v-model="address.street"
          type="text"
          placeholder="Улица"
          class="input"
        />
        <input
          v-model="address.house"
          type="text"
          placeholder="Дом"
          class="input"
        />
      </div>
    </div>
    <div class="passport">
      <h3 class="passport__title">Паспортные данные</h3>
      <select v-model="passport.type" class="passport__type-selector required">
        <option value="*" disabled>*</option>
        <option v-for="(type, index) in docTypes" :value="type.value">
          {{ type.label }}
        </option>
      </select>
      <div class="passport__number-wrapper">
        <input
          v-model="passport.seria"
          type="number"
          class="input"
          placeholder="Серия"
        />
        <input
          v-model="passport.number"
          type="number"
          class="input"
          placeholder="Номер"
        />
      </div>
      <input
        v-model="passport.whoIssued"
        type="text"
        placeholder="Кем выдан?"
        class="input"
      />
      <input
        v-model="passport.whenIssued"
        type="text"
        placeholder="Когда выдан? *"
        class="input required"
      />
    </div>
    <button class="form__submit-btn" type="submit">Зарегистрироваться</button>
  </form>
</template>
<style scoped lang="scss">
.form {
  margin-top: 20px;

  & > * {
    margin-bottom: 20px;
  }

  &__submit-btn {
    padding: 21px 40px;
    background-color: #42609b;
    border: none;
    border-radius: 5px;
    color: #fff;
    font-size: 18px;
    transition: linear 0.2s;

    &:hover {
      padding-left: 60px;
      padding-right: 60px;
      opacity: 0.7;
    }
  }
}
.input {
  padding: 14px 20px;
  box-sizing: border-box;
  background-color: transparent;
  font-size: 16px;
  color: #fff;
  border: 1px solid #3d3d3d;
  border-radius: 5px;

  &:focus {
    outline: 1px solid #4b72c2;
  }
}
.doctor {
  &__title {
    font-size: 18px;
  }
  &__selector {
    margin-top: 20px;
    padding: 10px;
    width: 80%;
    background-color: transparent;
    color: #fff;
    font-size: 18px;
    border: 1px solid #3d3d3d;
    border-radius: 4px;

    &:focus {
      outline: #4b72c2;
    }
  }
}
.group {
  & h3 {
    font-size: 18px;
  }
}
.sex {
  // @media (max-width: 500px) {
  //   display: flex;
  //   flex-direction: column;
  // }
}
.client-group {
  margin-top: 20px;
  padding: 10px 10px 0 10px;
  width: 100%;
  font-size: 16px;
  line-height: 20px;
  background-color: transparent;
  color: #7f7f7f;
  border: 1px solid #3d3d3d;

  &:focus {
    outline: 1px solid #4b72c2;
  }

  & > *:not(:last-child) {
    margin-bottom: 10px;
  }
  & > * {
    padding: 5px 10px;
    font-size: 18px;
    &:checked {
      background-color: #8b8b8b;
      border-radius: 3px;
    }
  }
}
.bio {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 30px;
  // flex-direction: column;

  @media (max-width: 530px) {
    gap: 15px;
  }

  & > * {
    flex: 1 1 45%;

    @media (max-width: 530px) {
      flex: 1 0 100%;
    }
  }
}
.address {
  margin-top: 40px;
  &__title {
    font-size: 24px;
    font-weight: 700;
  }
  &__inputs {
    margin-top: 20px;
    display: flex;
    flex-wrap: wrap;
    gap: 30px;

    @media (max-width: 530px) {
      gap: 15px;
    }

    & > * {
      flex: 1 0 48%;
    }
  }
}
.passport {
  margin-top: 30px;

  & > *:not(:first-child) {
    margin-top: 20px;
  }
  &__title {
    font-size: 25px;
    font-weight: 700;
  }
  &__type-selector {
    margin-top: 20px;
    padding: 10px;
    width: 80%;
    background-color: transparent;
    color: #fff;
    font-size: 18px;
    border: 1px solid #3d3d3d;
    border-radius: 4px;

    &:focus {
      outline: #4b72c2;
    }
  }
  &__number-wrapper {
    margin-top: 15px;
    display: flex;
    gap: 15px;

    @media (max-width: 530px) {
      flex-direction: column;
    }

    & > * {
      flex: 1 0 45%;
    }
  }
  & > input {
    display: block;
    width: 100%;
  }
}
.checkbox {
  position: relative;
  &__input {
    -webkit-appearance: none;
    appearance: none;
    width: 20px;
    height: 20px;
    position: absolute;
    top: -4px;
    z-index: 10;
    cursor: pointer;
  }

  &__label {
    padding-left: 40px;
    width: 25px;
    height: 25px;
    color: #7f7f7f;
    cursor: pointer;

    transition: color 0.5s ease-in;

    @media (max-width: 530px) {
      display: block;
      width: 100% !important;
    }

    &::before {
      margin-top: -5px;
      content: "";
      display: block;
      width: 25px;
      height: 25px;
      border: 1px solid #3d3d3d;

      border-radius: 4px;
      box-sizing: border-box;
      cursor: pointer;

      position: absolute;
      top: 0;
      left: 0;
      z-index: 1;

      transition: border 0.5s ease-in;
    }

    &::after {
      margin-top: -7px;
      content: "";
      display: block;
      width: 20px;
      height: 20px;

      background: url("/src/assets/checked-checkbox.png") no-repeat;
      background-size: cover;
      background-size: 20px 20px;
      opacity: 0;

      position: absolute;
      top: 4px;
      left: 2px;
      z-index: 4;

      transition: opacity 0.3s ease-in;
    }
  }

  &__input:checked + &__label::before {
    border: 1px solid #4b72c2;
  }

  &__input:checked + &__label {
    color: #4b72c2;
  }

  &__input:checked + &__label::after {
    opacity: 1 !important;
  }
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  /* display: none; <- Crashes Chrome on hover */
  -webkit-appearance: none;
  margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
}
</style>
