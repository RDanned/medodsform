<template>
  <div id="form" class="container">
    <h1>Форма подачи заявления</h1>

    <form-loading v-if="isLoading" />

    <form-success v-if="isSubmitted" />

    <form-error v-if="$v.$error">
      Проверьте форму и отправьте еще раз!
    </form-error>

    <form action="#" @submit.prevent="submit" v-if="!isLoading && !isSubmitted">
      <fieldset>
        <legend>Личный данные</legend>
        <form-error
          v-if="$v.personal.lastname.$dirty && !$v.personal.lastname.required"
        >
          Поле "Фамилия" обязательно для заполнения!
        </form-error>
        <div class="form-group">
          <label for="lastname">Фамилия <span class="required">*</span>:</label>
          <input
            type="text"
            name="lastname"
            id="lastname"
            placeholder="Фамилия"
            v-model.trim="$v.personal.lastname.$model"
          />
        </div>
        <form-error
          v-if="$v.personal.firstname.$dirty && !$v.personal.firstname.required"
        >
          Поле "Имя" обязательно для заполнения!
        </form-error>
        <div class="form-group">
          <label for="firstname">Имя<span class="required">*</span>:</label>
          <input
            type="text"
            name="firstname"
            id="firstname"
            placeholder="Имя"
            v-model.trim="$v.personal.firstname.$model"
          />
        </div>
        <div class="form-group">
          <label for="middlename">Отчество:</label>
          <input
            type="text"
            name="middlename"
            id="middlename"
            placeholder="Отчество"
            v-model.trim="personal.middlename"
          />
        </div>
        <form-error
          v-if="$v.personal.birthdate.$dirty && !$v.personal.birthdate.required"
        >
          Поле "Дата рождения" обязательно для заполнения!
        </form-error>
        <div class="form-group">
          <label for="birthdate"
            >Дата рождения<span class="required">*</span>:
          </label>
          <input
            type="date"
            name="birthdate"
            id="birthdate"
            v-model.trim="$v.personal.birthdate.$model"
          />
        </div>
        <form-error
          v-if="$v.personal.phone.$dirty && !$v.personal.phone.required"
        >
          Поле "Номер телефона" обязательно для заполнения!
        </form-error>
        <form-error
          v-if="
            $v.personal.phone.$dirty &&
              (!$v.personal.phone.length || !$v.personal.phone.numeric)
          "
        >
          Длина номера телефона должна составлять 11 цифр!
        </form-error>
        <div class="form-group">
          <label for="phone"
            >Номер телефона<span class="required">*</span>:
          </label>
          <input
            type="text"
            name="phone"
            id="phone"
            v-model.trim="$v.personal.phone.$model"
          />
        </div>
        <div class="form-group">
          <label for="gender">Пол:</label>
          <input
            type="text"
            name="gender"
            id="gender"
            placeholder="Укажите ваше гендерное сапоопределение"
            v-model.trim="personal.gender"
          />
        </div>

        <form-error
          v-if="$v.personal.type.$dirty && !$v.personal.type.required"
        >
          Выберите группу клиентов!
        </form-error>
        <div class="form-group">
          <label for="type">
            Группа клиентов <span class="required">*</span>:
          </label>
          <select
            name="type"
            id="type"
            multiple
            v-model.trim="$v.personal.type.$model"
          >
            <option value="VIP">
              VIP
            </option>
            <option value="Проблемные">
              Проблемные
            </option>
            <option value="ОМС">
              ОМС
            </option>
          </select>
        </div>
        <div class="form-group">
          <label for="doctor">
            Лечащий врач
          </label>
          <select name="doctor" id="doctor" v-model="personal.doctor">
            <option value="" selected disabled>
              --Выберите из списка--
            </option>
            <option value="Иванов">
              Иванов
            </option>
            <option value="Захаров">
              Захаров
            </option>
            <option value="Чернышева">
              Чернышева
            </option>
          </select>
        </div>
      </fieldset>

      <fieldset>
        <legend>Адресс</legend>
        <div class="form-group">
          <label for="country"> Страна: </label>
          <input
            type="text"
            name="country"
            id="country"
            placeholder="Страна"
            v-model="address.country"
          />
        </div>
        <div class="form-group">
          <label for="region"> Область: </label>
          <input
            type="text"
            name="region"
            id="region"
            placeholder="Область"
            v-model="address.region"
          />
        </div>

        <form-error v-if="$v.address.city.$dirty && !$v.address.city.required">
          Укажите ваш город!
        </form-error>
        <div class="form-group">
          <label for="city"> Город<span class="required">*</span>: </label>
          <input
            type="text"
            name="city"
            id="city"
            placeholder="Город"
            v-model.trim="$v.address.city.$model"
          />
        </div>
        <div class="form-group">
          <label for="street"> Улица: </label>
          <input
            type="text"
            name="street"
            id="street"
            placeholder="ул.Улица"
            v-model="address.street"
          />
        </div>
        <div class="form-group">
          <label for="house"> Дом: </label>
          <input
            type="text"
            name="house"
            id="house"
            placeholder="000"
            v-model="address.house"
          />
        </div>
        <div class="form-group">
          <label for="postal_code">Почтовый индекс: </label>
          <input
            type="text"
            name="postal_code"
            id="postal_code"
            placeholder="000000"
            v-model="address.postal_code"
          />
        </div>
      </fieldset>

      <fieldset>
        <legend>Паспортные данные</legend>

        <form-error v-if="$v.pass.type.$dirty && !$v.pass.type.required">
          Укажите тип документа!
        </form-error>
        <div class="form-group">
          <label for="pass_type">
            Тип документа <span class="required">*</span>
          </label>
          <select name="pass_type" id="pass_type" v-model="$v.pass.type.$model">
            <option value="" selected disabled>
              --Выберите из списка--
            </option>
            <option value="Паспорт">
              Паспорт
            </option>
            <option value="Свидетельство о рождении">
              Свидетельство о рождении
            </option>
            <option value="Водительское удостоверение">
              Водительское удостоверение
            </option>
          </select>
        </div>
        <div class="form-group">
          <label for="pass_serie"> Серия: </label>
          <input
            type="text"
            name="pass_serie"
            id="pass_serie"
            placeholder="00000000"
            v-model="pass.serie"
          />
        </div>
        <div class="form-group">
          <label for="pass_number"> Номер: </label>
          <input
            type="text"
            name="pass_number"
            id="pass_number"
            placeholder="00000000"
            v-model="pass.number"
          />
        </div>
        <div class="form-group">
          <label for="pass_serie"> Кем выдан: </label>
          <input
            type="text"
            name="pass_issuer"
            id="pass_issuer"
            placeholder="Кем выдан"
            v-model="pass.issuer"
          />
        </div>

        <form-error v-if="$v.pass.date.$dirty && !$v.pass.date.required">
          Укажите дату документа!
        </form-error>
        <div class="form-group">
          <label for="pass_serie">
            Дата выдачи <span class="required">*</span>:
          </label>
          <input
            type="date"
            name="pass_date"
            id="pass_date"
            v-model="$v.pass.date.$model"
          />
        </div>
      </fieldset>

      <fieldset>
        <div class="form-group nosms">
          <label for="nosms">Не отправлять СМС:</label>
          <input type="checkbox" name="nosms" id="nosms" v-model.trim="nosms" />
        </div>
        <div class="form-group">
          <input type="submit" name="submit" id="submit" value="Отправить" />
        </div>
      </fieldset>
    </form>
  </div>
</template>

<script>
import "@/assets/css/style.css";
import { required, numeric } from "vuelidate/lib/validators";
import FormError from "@/components/FormError";
import FormLoading from "@/components/FormLoading";
import FormSuccess from "@/components/FormSuccess";

export default {
  name: "App",
  components: { FormError, FormLoading, FormSuccess },
  data() {
    return {
      isSubmitted: false,
      isLoading: false,
      personal: {
        lastname: "",
        firstname: "",
        middlename: "",
        birthdate: "",
        phone: "",
        gender: "",
        type: [],
        doctor: "",
      },
      address: {
        postal_code: "",
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
      },
      pass: {
        type: "",
        serie: "",
        number: "",
        issuer: "",
        date: "",
      },
      nosms: false,
    };
  },
  validations: {
    personal: {
      lastname: {
        required,
      },
      firstname: {
        required,
      },
      birthdate: {
        required,
      },
      phone: {
        required,
        //between: between(5, 10),
        length: function(value) {
          return value.length === 11;
        },
        numeric,
      },
      type: { required },
    },
    address: {
      city: { required },
    },
    pass: {
      type: { required },
      date: { required },
    },
  },
  mounted() {
    this.$v.$reset();
    console.log(this.$v.$params);
  },
  methods: {
    submit: function() {
      this.$v.$touch();
      console.log(this.$v.personal.phone.between);
      console.log(this.$v.personal.phone.numeric);

      if (this.$v.$error) {
        document.querySelector("#form").scrollIntoView();
      } else {
        this.isLoading = true;

        setTimeout(function() {
          console.log("trrttrttttrrtrtrt");
        }, 2000);

        this.isLoading = false;
        this.isSubmitted = true;
      }
    },
  },
};
</script>

<style>
#form {
}
</style>
