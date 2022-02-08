<template>
  <form class="new-client-form" @submit="onSubmit">
    <h1>Новый Клиент</h1>
    <fieldset>
      <legend><img src="../assets/account-box.png" />Личные данные</legend>
      <label for="last-name">Фамилия</label>
      <input
        type="text"
        name="lastName"
        id="last-name"
        placeholder="обязательно"
        @input="setLastName($event.target.value)"
      />
      <template v-if="$v.lastName.$dirty">
        <div class="error-text" v-if="!$v.lastName.required">Поле не должно быть пустым</div>
        <div class="error-text" v-if="!$v.lastName.minLength">
          Поле должно содержать минимум 2 буквы
        </div>
      </template>
      <label for="first-name">Имя</label>
      <input
        type="text"
        name="firstName"
        id="first-name"
        placeholder="обязательно"
        @input="setFirstName($event.target.value)"
      />
      <template v-if="$v.firstName.$dirty">
        <div class="error-text" v-if="!$v.firstName.required">Поле не должно быть пустым</div>
        <div class="error-text" v-if="!$v.firstName.minLength">
          Поле должно содержать минимум 2 буквы
        </div>
      </template>
      <label for="middle-name">Отчество</label>
      <input
        type="text"
        name="middleName"
        id="middle-name"
        @input="setMiddleName($event.target.value)"
      />
      <label for="dob">Дата рождения</label>
      <input
        type="text"
        name="dob"
        id="dob"
        placeholder="ДД.ММ.ГГГГ обязательно"
        @input="setDOB($event.target.value)"
      />
      <template v-if="$v.dob.$dirty">
        <div class="error-date" v-if="!$v.dob.required">Поле не должно быть пустым</div>
        <div class="error-date" v-if="$v.dob.required && !$v.dob.dateInFormat">
          <p>Неверный формат даты</p>
          <p>(напр. 08.06.1988)</p>
        </div>
      </template>
      <label for="phone">Номер телефона</label>
      <input
        type="tel"
        name="phone"
        id="phone"
        placeholder="7********** обязательно"
        @input="setPhone($event.target.value)"
      />
      <template v-if="$v.phone.$dirty">
        <div class="error-phone" v-if="!$v.phone.required">Поле не должно быть пустым</div>
        <div class="error-phone" v-if="$v.phone.required && !$v.phone.phoneInFormat">
          <p>Неверный формат номера</p>
          <p>(напр. 79801234567)</p>
        </div>
      </template>
      <label for="gender">Пол</label>
      <select name="gender" id="gender" @input="setGender($event.target.value)">
        <option value="" selected disabled>Выберите пол</option>
        <option value="male">Муж.</option>
        <option value="female">Жен.</option>
      </select>
      <label for="group">Группа клиентов</label>
      <select multiple name="group" id="group" size="3" @input="setGroup($event)">
        <option value="vip">VIP</option>
        <option value="problem">Проблемные</option>
        <option value="oms">ОМС</option>
      </select>
      <div class="error-group" v-if="$v.group.$dirty && !$v.group.required">Не выбрана группа</div>
      <label for="doctor">Лечащий врач</label>
      <select name="doctor" id="doctor" @input="setDoctor($event.target.value)">
        <option value="" selected disabled>Выберите врача</option>
        <option value="Иванов">Иванов</option>
        <option value="Захаров">Захаров</option>
        <option value="Чернышева">Чернышева</option>
      </select>
      <label for="no-sms"
        >Не отправлять СМС
        <input
          type="checkbox"
          id="no-sms"
          name="noSMS"
          value="true"
          @input="setNoSMS($event.target.value)"
        />
        <span class="checkmark"></span>
      </label>
    </fieldset>
    <fieldset>
      <legend><img src="../assets/map-search.png" />Адрес</legend>
      <div class="address-container">
        <label for="zip-code"
          >Индекс
          <input
            type="text"
            name="zipCode"
            id="zip-code"
            @input="setZipCode($event.target.value)"
          />
          <template v-if="$v.zipCode.$dirty">
            <div class="error-zip" v-if="!$v.zipCode.numeric">Данное поле содежит только цифры</div>
            <div class="error-zip" v-if="!$v.zipCode.maxLength">
              Максимальная длина поля - 10 цифр
            </div>
          </template>
        </label>
        <label for="country"
          >Страна
          <input type="text" name="country" id="country" @input="setCountry($event.target.value)" />
        </label>
      </div>
      <label for="oblast">Область</label>
      <input type="text" name="oblast" id="oblast" @input="setOblast($event.target.value)" />
      <label for="city">Город</label>
      <input
        type="text"
        name="city"
        id="city"
        placeholder="обязательно"
        @input="setCity($event.target.value)"
      />
      <template v-if="$v.city.$dirty">
        <div class="error-text" v-if="!$v.city.required">Поле не должно быть пустым</div>
        <div class="error-text" v-if="!$v.city.minLength">
          Поле должно содержать минимум 2 буквы
        </div>
      </template>
      <div class="address-container">
        <label for="street"
          >Улица
          <input type="text" name="street" id="street" @input="setStreet($event.target.value)" />
        </label>
        <label for="house"
          >Дом
          <input type="text" name="house" id="house" @input="setHouse($event.target.value)" />
          <div class="error-house" v-if="$v.house.$dirty && !$v.house.maxLength">
            Максимальная длина поля - 4 символа
          </div>
        </label>
      </div>
    </fieldset>
    <fieldset>
      <legend><img src="../assets/card-account-details.png" />Документ</legend>
      <label for="document">Тип документа</label>
      <select
        name="document"
        id="document"
        @input="setDocument($event.target.value)"
        @blur="setDocument($event.target.value)"
      >
        <option value="" disabled selected>Выберите тип документа</option>
        <option value="passport">Паспорт</option>
        <option value="birthCert">Свидетельство о рождении</option>
        <option value="driversLicense">Вод. удостоверение</option>
      </select>
      <div class="error-document" v-if="$v.document.$dirty && !$v.document.required">
        Не выбран документ
      </div>
      <div class="doc-container">
        <label for="doc-series"
          >Серия
          <input
            type="text"
            name="docSeries"
            id="doc-series"
            @input="setDocSeries($event.target.value)"
          />
          <div class="error-series" v-if="$v.docSeries.$dirty && !$v.docSeries.maxLength">
            Макс. длина поля - 4 символа
          </div>
        </label>
        <label for="doc-number"
          >Номер
          <input
            type="text"
            name="docNumber"
            id="doc-number"
            @input="setDocNumber($event.target.value)"
          />
        </label>
      </div>
      <label for="issued-by">Кем выдан</label>
      <input type="text" name="issuedBy" id="issued-by" @input="setIssuedBy($event.target.value)" />
      <label for="issue-date">Дата выдачи</label>
      <input
        type="text"
        name="issueDate"
        id="issue-date"
        placeholder="ДД.ММ.ГГГГ обязательно"
        @input="setIssueDate($event.target.value)"
      />
      <template v-if="$v.issueDate.$dirty">
        <div class="error-date" v-if="!$v.issueDate.required">Поле не должно быть пустым</div>
        <div class="error-date" v-if="$v.issueDate.required && !$v.issueDate.dateInFormat">
          <p>Неверный формат даты</p>
          <p>(напр. 08.06.1988)</p>
        </div>
      </template>
    </fieldset>
    <div class="submit-error" v-if="submitStatus === 'ERROR'">
      Клиент не создан. Проверьте правильность заполнения формы.
    </div>
    <input type="submit" value="Создать Клиента" />
  </form>
</template>

<script>
import { required, minLength, maxLength, numeric } from 'vuelidate/lib/validators'

const dateInFormat = (date) => {
  const day = date.slice(0, 2)
  const month = date.slice(3, 5)
  const year = date.slice(6)
  if (day > 0 && day < 32 && month > 0 && month < 13 && year > 1900 && year < 2100) {
    return true
  }
  return false
}

const phoneInFormat = (phone) => {
  const regex = /[7]\d{10}/
  if (phone.length > 11) {
    return false
  }
  return regex.test(phone)
}

const resetData = () => {
  return {
    lastName: '',
    firstName: '',
    middleName: '',
    dob: '',
    phone: '',
    gender: '',
    group: [],
    doctor: '',
    noSMS: false,
    zipCode: '',
    country: '',
    oblast: '',
    city: '',
    street: '',
    house: '',
    document: '',
    docSeries: '',
    docNumber: '',
    issuedBy: '',
    issueDate: '',
    submitStatus: 'OK',
  }
}

export default {
  data: () => {
    return resetData()
  },
  validations: {
    lastName: { required, minLength: minLength(2) },
    firstName: { required, minLength: minLength(2) },
    dob: { required, dateInFormat },
    phone: { required, phoneInFormat },
    group: { required },
    zipCode: { numeric, maxLength: maxLength(10) },
    city: { required, minLength: minLength(2) },
    house: { maxLength: maxLength(4) },
    document: { required },
    docSeries: { maxLength: maxLength(4) },
    issueDate: { required, dateInFormat },
  },
  methods: {
    setLastName(value) {
      this.lastName = value
      this.$v.lastName.$touch()
    },
    setFirstName(value) {
      this.firstName = value
      this.$v.firstName.$touch()
    },
    setMiddleName(value) {
      this.lastName = value
    },
    setDOB(value) {
      this.dob = value
      this.$v.dob.$touch()
    },
    setPhone(value) {
      this.phone = value
      this.$v.phone.$touch()
    },
    setGender(value) {
      this.gender = value
    },
    setGroup(e) {
      const groupSelector = e.target
      const groups = groupSelector.selectedOptions
      this.group = []
      for (let i = 0; i < groups.length; i++) {
        if (this.group.indexOf(groups[i].label) === -1) {
          this.group.push(groups[i].label)
        }
      }
      this.$v.group.$touch()
    },
    setDoctor(value) {
      this.doctor = value
    },
    setNoSMS(value) {
      this.noSMS = value
      console.log(this.noSMS)
    },
    setZipCode(value) {
      this.zipCode = value
      this.$v.zipCode.$touch()
    },
    setCountry(value) {
      this.country = value
    },
    setOblast(value) {
      this.oblast = value
    },
    setCity(value) {
      this.city = value
      this.$v.city.$touch()
    },
    setStreet(value) {
      this.street = value
    },
    setHouse(value) {
      this.house = value
      this.$v.house.$touch()
    },
    setDocument(value) {
      this.document = value
      this.$v.document.$touch()
    },
    setDocSeries(value) {
      this.docSeries = value
      this.$v.docSeries.$touch()
    },
    setDocNumber(value) {
      this.docNumber = value
      this.$v.docNumber.$touch()
    },
    setIssuedBy(value) {
      this.issuedBy = value
    },
    setIssueDate(value) {
      this.issueDate = value
      this.$v.issueDate.$touch()
    },
    onSubmit(e) {
      e.preventDefault()
      this.$v.$touch()
      if (this.$v.$invalid) {
        this.submitStatus = 'ERROR'
      } else {
        this.submitStatus = 'OK'
        this.$v.$reset()
        this.$el.reset()
        Object.assign(this.$data, resetData())
      }
    },
  },
}
</script>
