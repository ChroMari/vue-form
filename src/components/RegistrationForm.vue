<template>
<div>
  <RegistrationPopup 
    v-if="showModal" />
  <form 
    class="vue-form" 
    @submit.prevent="submitForm" 
    v-if="!showModal">
    <fieldset>
      <div>
        <label 
          class="label" 
          for="surname">Фамилия*
          <span 
            v-if="$v.formValidationRegist.surname.$dirty && !$v.formValidationRegist.surname.required">
            Поле должно быть заполнено
          </span>
        </label>
        <input 
          type="text" 
          id="surname" 
          v-model.trim="formValidationRegist.surname"
          :class="{invalid: ($v.formValidationRegist.surname.$dirty && !$v.formValidationRegist.surname.required)}"
          placeholder="Иванов">
      </div>
      <div>
        <label 
          class="label" 
          for="name">Имя*
          <span 
            v-if="$v.formValidationRegist.name.$dirty && !$v.formValidationRegist.name.required">
            Поле должно быть заполнено
          </span>
        </label>
        <input 
          type="text" 
          id="name" 
          v-model.trim="formValidationRegist.name"
          :class="{invalid: ($v.formValidationRegist.name.$dirty && !$v.formValidationRegist.name.required)}"
          placeholder="Иван">
      </div>
      <div>
        <label 
          class="label" 
          for="patronymic">
          Отчество
        </label>
        <input 
          type="text" 
          id="patronymic" 
          v-model.trim="formValidationRegist.patronymic"
          placeholder="Иванович">
      </div>
      <div>
        <label 
          class="label" 
          for="birthday">
          Дата рождения*
          <span 
            v-if="$v.formValidationRegist.birthday.$dirty && !$v.formValidationRegist.birthday.required">
            Поле должно быть заполнено
          </span>
        </label>
        <input 
          type="date" 
          :class="{invalid: ($v.formValidationRegist.birthday.$dirty && !$v.formValidationRegist.birthday.required)}" 
          v-model="formValidationRegist.birthday">
      </div>
      <div>
        <label 
          class="label" 
          for="phone">
          Номер телефона*
          <span 
            v-if="$v.formValidationRegist.phone.$dirty && !$v.formValidationRegist.phone.required">
            Поле должно быть заполнено
          </span>
          <span 
            v-else-if="$v.formValidationRegist.phone.$dirty && !$v.formValidationRegist.phone.minLength">
            Введите полностью номер телефона
          </span>
        </label>
        <div 
          class="input-group" 
          :class="{invalid: ($v.formValidationRegist.phone.$dirty && !$v.formValidationRegist.phone.required) || ($v.formValidationRegist.phone.$dirty && !$v.formValidationRegist.phone.minLength)}">
          <span 
            class="input-group-addon">
            <span>+7</span>
          </span>
          <input 
            type="tel" 
            v-model="formValidationRegist.phone" 
            name="phone" 
            id="phone" 
            placeholder="(555) 555-5555" 
            autocomplete="tel" 
            class="form-control" 
            v-phone/>
        </div>
      </div>
      <div>
        <label 
          class="label" 
          for="gendere">
          Пол
        </label>
        <ul class="vue-form-list">
          <li>
            <input 
              type="radio" 
              name="radio-1" 
              id="radio-1" 
              value="man" 
              v-model="formValidationRegist.gendere">
            <label 
              for="radio-1">
              Мужчина
            </label>
          </li>
          <li>
            <input 
              type="radio" 
              name="radio-2" 
              id="radio-2" 
              value="woman" 
              v-model="formValidationRegist.gendere">
            <label 
              for="radio-2">
              Женщина
            </label>
          </li>
        </ul>
      </div>
      <div>
        <label 
          class="label" 
          for="groupClient">
          Группа клиентов*
          <span 
            v-if="$v.formValidationRegist.groupClient.$dirty && !$v.formValidationRegist.groupClient.required">
            Поле должно быть выбрано
          </span>
        </label>
        <select 
          id="groupClient" 
          class="budget budget-multiple" 
          multiple 
          v-model="formValidationRegist.groupClient" 
          :class="{invalid: ($v.formValidationRegist.groupClient.$dirty && !$v.formValidationRegist.groupClient.required)}">
          <option 
            v-for="(client, index) in groupClients" 
            :value="client.value" 
            :key="index">
            {{ client.label }} 
          </option>
        </select>
      </div>
      <div>
        <label 
          class="label" 
          for="doct">
          Лечащий врач
        </label>
        <p class="select">
          <select 
            id="doct" 
            class="budget" 
            v-model="formValidationRegist.doctor">
            <option 
              v-for="(doc, index) in doctors" 
              :value="doc.value" 
              :key="index">
              {{ doc.label }}
            </option>
          </select>
        </p>
      </div>
      <div>
        <input 
          type="checkbox" 
          :value="formValidationRegist.checkSMS" 
          id="cb-feature-1" 
          v-model="formValidationRegist.checkSMS">
        <label for="cb-feature-1">Не отправлять СМС</label>
      </div>

      <h4 class="vue-form__legend">Адрес</h4>

      <div>
        <label 
          class="label" 
          for="indexRussia">
          Индекс
          <span 
            v-if="(formValidationRegist.indexRussia.length != 6 && formValidationRegist.indexRussia.length != 0)">
            Индекс должен состоять из 6 символов
          </span>
        </label>
        <input 
          type="text" 
          id="indexRussia" 
          v-model.trim="formValidationRegist.indexRussia"
          :class="{invalid: (formValidationRegist.indexRussia.length != 6 && formValidationRegist.indexRussia.length != 0)}"
          placeholder="123456">
      </div>
      <div>
        <label 
          class="label" 
          for="indexRussia">
          Страна
        </label>
        <input 
          type="text" 
          id="indexRussia" 
          v-model.trim="formValidationRegist.country"
          placeholder="Россия">
      </div>
      <div>
        <label 
          class="label" 
          for="indexRussia">
          Область
        </label>
        <input 
          type="text" 
          id="surname" 
          v-model.trim="formValidationRegist.region"
          placeholder="Ивановская">
      </div>
      <div>
        <label 
          class="label" 
          for="city">
          Город*
          <span 
            v-if="$v.formValidationRegist.city.$dirty && !$v.formValidationRegist.city.required">
            Поле должно быть заполнено</span>
        </label>
        <input 
          type="text" 
          id="city" 
          v-model.trim="formValidationRegist.city"
          :class="{invalid: ($v.formValidationRegist.city.$dirty && !$v.formValidationRegist.city.required)}"
          placeholder="Шуя">
      </div>
      <div>
        <label 
          class="label" 
          for="street">
          Улица
        </label>
        <input
          type="text" 
          id="street" 
          v-model.trim="formValidationRegist.street"
          placeholder="Гагарина">
      </div>
      <div>
        <label 
          class="label" 
          for="house">
          Дом
        </label>
        <input 
          type="text" 
          id="house" 
          v-model.trim="formValidationRegist.house"
          placeholder="8">
      </div>

      <h4 class="vue-form__legend">Паспорт</h4>

      <div>
        <label 
          class="label" 
          for="document">Тип документа*
          <span 
            v-if="$v.formValidationRegist.document.$dirty && !$v.formValidationRegist.document.required">
            Поле должно быть выбрано
          </span>
        </label>
        <p class="select">
          <select 
            id="document" 
            class="budget" 
            v-model="formValidationRegist.document" 
            :class="{invalid: ($v.formValidationRegist.document.$dirty && !$v.formValidationRegist.document.required)}">
            <option 
              v-for="(docum, index) in documents" 
              :value="docum.value" 
              :key="index">
              {{ docum.label }}
            </option>
          </select>
        </p>
      </div>
      <div>
        <label 
          class="label" 
          for="documentSeria">
          Серия
          <span 
            v-if="(formValidationRegist.document_seria.length != 4 && formValidationRegist.document_seria.length != 0)">
            Серия паспорта состоит из 4 символов
          </span>
          <span 
            v-else-if="(!/^-{0,1}\d+$/.test(formValidationRegist.document_seria) && formValidationRegist.document_seria.length != 0)">
            Серия паспорта состоит только из чисел
          </span>
        </label>
        <input 
          type="text" 
          id="documentSeria" 
          v-model.trim="formValidationRegist.document_seria" 
          :class="{invalid: (formValidationRegist.document_seria.length != 4 && formValidationRegist.document_seria.length != 0) || (!/^-{0,1}\d+$/.test(formValidationRegist.document_seria) && formValidationRegist.document_seria.length != 0)}"
          placeholder="1234">
      </div>
      <div>
        <label 
          class="label" 
          for="documentNumber">
          Номер
          <span 
            v-if="(formValidationRegist.document_number.length != 6 && formValidationRegist.document_number.length != 0)">
            Номер паспорта состоит из 6 символов
          </span>
          <span 
            v-else-if="(!/^-{0,1}\d+$/.test(formValidationRegist.document_number) && formValidationRegist.document_number.length != 0)">
            Номер паспорта состоит только из чисел
          </span>
        </label>
        <input 
          type="text" 
          id="documentNumber" 
          v-model.trim="formValidationRegist.document_number" 
          :class="{invalid: (formValidationRegist.document_number.length != 6 && formValidationRegist.document_number.length != 0) || (!/^-{0,1}\d+$/.test(formValidationRegist.document_number) && formValidationRegist.document_number.length != 0)}"
          placeholder="123456">
      </div>
      <div>
        <label 
          class="label" 
          for="issued">
          Кем выдан
        </label>
        <input 
          type="text" 
          id="issued" 
          v-model.trim="formValidationRegist.issued">
      </div>
      <div>
        <label 
          class="label" 
          for="issuedDay">
          Дата выдачи*
          <span 
            v-if="$v.formValidationRegist.issued_day.$dirty && !$v.formValidationRegist.issued_day.required">
            Поле должно быть заполнено
           </span>
        </label>
        <input 
          type="date" 
          :class="{invalid: ($v.formValidationRegist.issued_day.$dirty && !$v.formValidationRegist.issued_day.required)}" 
          v-model="formValidationRegist.issued_day">
      </div>

      <p class="info">* - Поле обязательное для заполнения.</p>
        
      <div>
        <input 
          type="submit" 
          value="Создать">
      </div>
    </fieldset>
  </form>
</div>
</template>

<script>
import { required, minLength } from 'vuelidate/lib/validators';
import RegistrationPopup from './RegistrationPopup.vue';

export default {
  name: 'RegistrationForm',
  components: {
    RegistrationPopup,
  },
  data: () => ({
    formValidationRegist: {
      surname: '',
      name: '',
      patronymic: '',
      birthday: '',
      phone: '',
      gendere: 'man',
      groupClient: [],
      doctor: '',
      checkSMS: false,
      indexRussia: '',
      country: '',
      region: '',
      city: '',
      street: '',
      house: '',
      document: '',
      document_seria: '',
      document_number: '',
      issued: '',
      issued_day: '',
    },
    groupClients: [
      {
        label: 'VIP',
        value: 'VIP',
      },
      {
        label: 'Проблемные',
        value: 'Problems',
      },
      {
        label: 'ОМС',
        value: 'OMS',
      }
    ],
    doctors:[
      {
        label: 'Иванов',
        value: 'Ivanov',
      },
      {
        label: 'Захаров',
        value: 'Zakharov',
      },
      {
        label: 'Чернышова',
        value: 'Chernyshova',
      },
    ],
    documents:[
      {
        label: 'Паспорт',
        value: 'passport',
      },
      {
        label: 'Свидетельство о рождении',
        value: 'birth_certificate',
      },
      {
        label: 'Вод. удостоверение',
        value: 'drivers_license',
      },
    ],
    showModal: false,
  }),
  directives: {
    phone: {
      bind(el) {
        el.oninput = function(e) {
          if (!e.isTrusted) return;
          const x = this.value.replace(/\D/g, '').match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
          this.value = !x[2] ? x[1] : '(' + x[1] + ') ' + x[2] + (x[3] ? '-' + x[3] : '');
          el.dispatchEvent(new Event('input'));
        }
      },
    },
  },
  validations: {
    formValidationRegist: {
      surname: { required },
      name: { required },
      birthday: { required },
      phone: { required, minLength: minLength(14) },
      groupClient: { required },
      city: { required },
      document: { required },
      issued_day: { required },
    },
  },
  methods: {
    submitForm() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      else {
        const formData = {
          surname: this.formValidationRegist.surname,
          name: this.formValidationRegist.name,
          patronymic: this.formValidationRegist.patronymic,
          birthday: this.formValidationRegist.birthday,
          phone: '7' + this.formValidationRegist.phone,
          gendere: this.formValidationRegist.gendere,
          groupClient: this.formValidationRegist.groupClient,
          doctor: this.formValidationRegist.doctor,
          checkSMS: this.formValidationRegist.checkSMS,
          indexRussia: this.formValidationRegist.indexRussia,
          country: this.formValidationRegist.country,
          region: this.formValidationRegist.region,
          city: this.formValidationRegist.city,
          street: this.formValidationRegist.street,
          house: this.formValidationRegist.house,
          document: this.formValidationRegist.document,
          document_seria: this.formValidationRegist.document_seria,
          document_number: this.formValidationRegist.document_number,
          issued: this.formValidationRegist.issued,
          issued_day: this.formValidationRegist.issued_day,
        };
        console.log(formData);
        this.showModal = true;
      }
    },
  },
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css?family=Source+Code+Pro:300,400");
@import '../assets/style/RegistrationForm.sass';

</style>
