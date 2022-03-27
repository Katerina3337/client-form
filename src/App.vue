<template>
  <div id="app">
    <div class="container">
      <h1 class="form-headline">Форма создания клиента</h1>

      <form action="">
        <fieldset>
          <legend>Клиент</legend>
          <div class="form-item" :class="{ 'form-group--error': $v.surname.$error }">
            <label for="surname">Фамилия*</label>
            <input v-model="$v.surname.$model" type="text" id="surname" />
          </div>
          <div class="form-item" :class="{ 'form-group--error': $v.name.$error }">
            <label for="name">Имя*</label>
            <input v-model.trim="$v.name.$model" type="text" id="name" />
          </div>
          <div class="form-item">
            <label for="patronymic">Отчество</label>
            <input v-model="patronymic" type="text" id="patronymic" />
          </div>
          <div class="form-item" :class="{ 'form-group--error': $v.birth.$error }">
            <label for="birth">Дата рождения*</label>
            <input v-model.trim="$v.birth.$model" type="date" id="birth" />
          </div>
          <div class="form-item" :class="{ 'form-group--error': $v.tel.$error }">
            <label for="tel">Номер телефона*</label>
            <div>
              <input v-model.trim="$v.tel.$model" type="tel" id="tel" />
              <p class="notice">*11 цифр. Начинается с 7</p>
            </div>

          </div>
          <div class="form-item">
            <label for="gender">Пол</label>
            <select v-model="gender" id="gender">
              <option value="1">Мужской</option>
              <option value="0">Женский</option>
            </select>
          </div>
          <div class="form-item" :class="{ 'form-group--error': $v.client_group.$error }">
            <label for="client_group">Группа клиентов*</label>
            <select
              style="height: 55px; overflow: hidden"
              v-model.trim="$v.client_group.$model"
              id="client_group"
              multiple
            >
              <option value="1">VIP</option>
              <option value="2">Проблемные</option>
              <option value="3">ОМС</option>
            </select>
          </div>
          <div class="form-item">
            <label for="doctor">Лечащий врач</label>
            <select v-model="doctor" id="doctor">
              <option value="1">Иванов</option>
              <option value="2">Захаров</option>
              <option value="3">Чернышева</option>
            </select>
          </div>
          <div class="form-item">
            <label for="dont_send_email">Не отправлять СМС</label>
            <input
              v-model="dont_send_email"
              id="dont_send_email"
              type="checkbox"
            />
          </div>
        </fieldset>

        <fieldset>
          <legend>Адрес</legend>
          <div class="form-item">
            <label for="post_index">Индекс</label>
            <input v-model="post_index" type="number" id="post_index" />
          </div>
          <div class="form-item">
            <label for="country">Страна</label>
            <input v-model="country" type="text" id="country" />
          </div>
          <div class="form-item">
            <label for="region">Область</label>
            <input v-model="region" type="text" id="region" />
          </div>
          <div class="form-item" :class="{ 'form-group--error': $v.city.$error }">
            <label for="city">Город*</label>
            <input v-model.trim="$v.city.$model" type="text" id="city" />
          </div>
          <div class="form-item">
            <label for="street">Улица</label>
            <input v-model="street" type="text" id="street" />
          </div>
          <div class="form-item">
            <label for="house">Дом</label>
            <input v-model="house" type="number" id="house" />
          </div>
        </fieldset>
        <fieldset>
          <legend>Паспорт</legend>
          <div class="form-item" :class="{ 'form-group--error': $v.document_type.$error }">
            <label for="document_type">Тип документа*</label>
            <select v-model.trim="$v.document_type.$model" id="document_type">
              <option value="1">Паспорт</option>
              <option value="2">Свидетельство о рождении</option>
              <option value="3">Вод. удостоверение</option>
            </select>
          </div>
          <div class="form-item">
            <label for="document_series">Серия</label>
            <input
              v-model="document_series"
              type="number"
              id="document_series"
            />
          </div>
          <div class="form-item">
            <label for="document_number">Номер</label>
            <input
              v-model="document_number"
              type="number"
              id="document_number"
            />
          </div>
          <div class="form-item">
            <label for="document_issued">Кем выдан</label>
            <input v-model="document_issued" type="text" id="document_issued" />
          </div>
          <div class="form-item"  :class="{ 'form-group--error': $v.document_issue_date.$error }">
            <label for="document_issue_date">Дата выдачи*</label>
            <input
              v-model.trim="$v.document_issue_date.$model"
              type="date"
              id="document_issue_date"
            />
          </div>
        </fieldset>

        <p class="notice">*Поля обязательные для заполнения.</p>

        
        <div class="notifications">
          <h3 class="error-message" v-if="errorMessage">{{errorMessage}}</h3>
          <h3 class="success-message" v-if="successMessage">{{successMessage}}</h3>
        </div>
        
        <button class="add-client" @click.prevent="getData">
          Создать клиента
        </button>
      </form>
    </div>
  </div>
</template>

<script>

import { required } from 'vuelidate/lib/validators';
import { helpers } from 'vuelidate/lib/validators';

const phone = helpers.regex('phone', /^((7)+([0-9]){10})$/);


export default {
  name: "App",
  data(){
    return{
      errorMessage: "",
      successMessage: "",


      surname: "",
      name: "",
      patronymic: "",
      birth: "",
      tel: "",
      gender: 1,
      client_group: [],
      doctor: "",
      dont_send_email: "",
      post_index: "",
      country: "",
      region: "",
      city: "",
      street: "",
      house: "",
      document_type: "",
      document_series: "",
      document_number: "",
      document_issued: "",
      document_issue_date: "",
    }
  },
  validations: {
    surname: {
      required,
    },
    name: {
      required,
    },
    birth: {
      required,
    },
    tel: {
      required,
      phone
    },
    client_group: {
      required,
    },
    city: {
      required,
    },
    document_type: {
      required,
    },
    document_issue_date: {
      required,
    },
  },
  methods: {
    getData() {
      this.$v.$touch();
      console.log(this.$v);
      if (this.$v.$invalid) {
        this.errorMessage = 'Заполните все поля корректно!'
      }else{
        this.successMessage = 'Новый клиент успешно создан!'
      }

      setTimeout(() => {
        this.errorMessage = "";
        this.successMessage = "";
      }, 1500)
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
