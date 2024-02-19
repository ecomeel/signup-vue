<script>
// import Input from "../input/Input.vue";
// import AboutPerson from "../aboutPerson/AboutPerson.vue";
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
        doctor: "",
        agreeGetMessages: true,
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
    };
  },
};
</script>
<template>
  <form class="form">
    <div class="bio">
      <input
        class="input"
        v-model.trim="about.name"
        placeholder="Имя"
        type="text"
      />
      <input
        class="input"
        v-model.trim="about.surname"
        placeholder="Фамилия"
        type="text"
      />
      <input
        class="input"
        v-model.trim="about.partonymic"
        placeholder="Отчество"
        type="text"
      />
      <input
        class="input"
        v-model.trim="about.birthDay"
        placeholder="Дата рождения"
        type=""
      />
      <input
        class="input"
        v-model.trim="about.phone"
        placeholder="Номер телефона"
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
        <h3>Выберите группу клиента:</h3>
        <select class="client-group" v-model="about.clientGroup" multiple>
          <label>Группа клиентов</label>
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
        />
        <label class="checkbox__label">Желаете получать СМС уведомления?</label>
      </div>
    </div>
    <div class="address">
      <h2 class="address__title">Адресс</h2>
      <div class="address__inputs">
        <input type="text" placeholder="Индекс" class="input" />
        <input type="text" placeholder="Страна" class="input" />
        <input type="text" placeholder="Область" class="input" />
        <input type="text" placeholder="Город" class="input" />
        <input type="text" placeholder="Улица" class="input" />
        <input type="text" placeholder="Дом" class="input" />
      </div>
    </div>
    <div class="passport">
      <h3 class="passport__title">Паспортные данные</h3>
      <select class="passport__type-selector">
        <option value="">Паспорт</option>
        <option value="">Свидетельство о рождении</option>
        <option value="">Вод. удостоверение</option>
      </select>
    </div>
  </form>
</template>
<style scoped lang="scss">
.form {
  margin-top: 20px;

  & > * {
    margin-bottom: 20px;
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
  // display: flex;
  &__title {
    font-size: 18px;
  }
  &__selector {
    margin-top: 20px;
    padding: 5px;
    width: 80%;
    background-color: transparent;
    color: #fff;
    font-size: 18px;

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
.client-group {
  margin-top: 20px;
  padding: 10px;
  width: 100%;
  font-size: 16px;
  line-height: 20px;
  background-color: transparent;
  color: #fff;
  border: 1px solid #3d3d3d;

  &:focus {
    outline: 1px solid #4b72c2;
  }

  & > *:not(:last-child) {
    margin-bottom: 10px;
  }
  & > * {
    font-size: 20px;
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

  & > * {
    flex: 1 1 45%;
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

    & > * {
      flex: 1 0 48%;
    }
  }
}
.passport {
  margin-top: 30px;
  &__title {
    font-size: 25px;
    font-weight: 700;
  }
  &__type-selector {

  }
}
.checkbox {
  position: relative;
  &__input {
    -webkit-appearance: none;
    appearance: none;
    width: 24px;
    height: 24px;
    position: absolute;
    top: -4px;
    z-index: 10;
    cursor: pointer;
  }

  &__label {
    padding-left: 40px;
    width: 30px;
    height: 30px;
    color: #7f7f7f;
    cursor: pointer;

    transition: color 0.5s ease-in;

    &::before {
      margin-top: -5px;
      content: "";
      display: block;
      width: 30px;
      height: 30px;
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
      width: 24px;
      height: 24px;

      background: url("/src/assets/checked-checkbox.png") no-repeat;
      background-size: cover;
      background-size: 28px 28px;
      opacity: 0;

      position: absolute;
      top: 2px;
      left: 2px;
      z-index: 4;

      transition: opacity 0.5s ease-in;
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
</style>
