<template>
  <form class="new-client-form">
    <h1>Новый Клиент</h1>
    <fieldset>
      <legend><img src="../assets/account-box.png" />Личные данные</legend>
      <label for="last-name">Фамилия</label>
      <input type="text" name="lastName" id="last-name" placeholder="обязательно" />
      <label for="first-name">Имя</label>
      <input type="text" name="firstName" id="first-name" placeholder="обязательно" />
      <label for="middle-name">Отчество</label>
      <input type="text" name="middleName" id="middle-name" />
      <label for="dob">Дата рождения</label>
      <input type="text" name="dob" id="dob" placeholder="ДД.ММ.ГГГГ обязательно" />
      <label for="phone">Номер телефона</label>
      <input type="tel" name="phone" id="phone" placeholder="7********** обязательно" />
      <label for="gender">Пол</label>
      <select name="gender" id="gender">
        <option value="" selected disabled>Выберите пол</option>
        <option value="male">Муж.</option>
        <option value="female">Жен.</option>
      </select>
      <label for="group">Группа клиентов</label>
      <select multiple name="group" id="group" size="3">
        <option value="vip">VIP</option>
        <option value="problem">Проблемные</option>
        <option value="oms">ОМС</option>
      </select>
      <label for="sms"
        >Не отправлять СМС
        <input type="checkbox" id="sms" name="sms" />
        <span class="checkmark"></span>
      </label>
    </fieldset>
    <fieldset>
      <legend><img src="../assets/map-search.png" />Адрес</legend>
      <div class="address-container">
        <label for="zip-code"
          >Индекс
          <input type="text" name="zipCode" id="zip-code" />
        </label>
        <label for="country"
          >Страна
          <input type="text" name="country" id="country" />
        </label>
      </div>
      <label for="oblast">Область</label>
      <input type="text" name="oblast" id="oblast" />
      <label for="city">Город</label>
      <input type="text" name="city" id="city" placeholder="обязательно" />
      <div class="address-container">
        <label for="street"
          >Улица
          <input type="text" name="street" id="street" />
        </label>
        <label for="house"
          >Дом
          <input type="text" name="house" id="house" />
        </label>
      </div>
    </fieldset>
    <fieldset>
      <legend><img src="../assets/card-account-details.png" />Документ</legend>
      <label for="document">Тип документа</label>
      <select name="document" id="document">
        <option value="" disabled selected>Выберите тип документа</option>
        <option value="passport">Паспорт</option>
        <option value="birthCert">Свидетельство о рождении</option>
        <option value="driversLicense">Вод. удостоверение</option>
      </select>
      <div class="doc-container">
        <label for="doc-series"
          >Серия
          <input type="text" name="docSeries" id="doc-series" />
        </label>
        <label for="doc-number"
          >Номер
          <input type="text" name="docNumber" id="doc-number" />
        </label>
      </div>
      <label for="issued-by">Кем выдан</label>
      <input type="text" name="issuedBy" id="issued-by" />
      <label for="issue-date">Дата выдачи</label>
      <input type="text" name="issueDate" id="issue-date" placeholder="ДД.ММ.ГГГГ обязательно" />
    </fieldset>
    <input type="submit" value="Создать Клиента" />
  </form>
</template>

<script>
export default {}
</script>
