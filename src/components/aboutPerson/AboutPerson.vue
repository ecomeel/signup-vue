<script>
export default {
  // props: {about: {name: string}},
  props: ["name", "surname"],
  data() {
    return {};
  },
};
</script>
<template>
  <div>
    <input class="input" v-model="name" placeholder="Имя" type="text" />
    <input class="input" placeholder="Фамилия" type="text" />
    <!-- <input
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
    <select v-model="about.clientGroup" multiple>
      <option
        v-for="(group, index) in clientGroups"
        :key="index"
        :value="group.value"
      >
        {{ group.label }}
      </option>
    </select>
    <select v-model="about.doctor">
      <option
        v-for="(doctor, index) in doctors"
        :key="index"
        :value="doctor.value"
      >
        {{ doctor.label }}
      </option>
    </select>
    <label>
      Желаете получать СМС уведомления?
      <input v-model="about.agreeGetMessages" type="checkbox" />
    </label> -->
  </div>
</template>
