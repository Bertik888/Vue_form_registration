<template>
  <form 
    class="form-block"
    @submit.prevent="onSubmit"
  >
    <div class="form-block__title">Регистрация</div>
    <hr class="form-block__line">
    <div class="form-block__subtitle">
      Заполните Ваши данные
    </div>
    <div class="form-block__row">
      <div class="form-block__col">
        <ui-input
          v-model="form.user_name" 
          placeholder="Имя"
          :invalidText="invalidUserNameText"
        />
        <ui-input
          v-model="form.password" 
          type="password"
          placeholder="Пароль"
          :invalidText="invalidPasswordText"
          class="mt-auto"
        />
      </div>
      <div class="form-block__col">
        <ui-input 
          v-model="form.email" 
          placeholder="Email"
          :invalidText="invalidEmailText"
          class="mb-31"
        />
        <ui-select 
          v-model="form.role" 
          :options="optionSelect"          
          :invalidText="invalidSelectText"
          label="Должность"
          class="mb-31"
        />
        <ui-input 
          v-model="form.password_repeat" 
          type="password"
          placeholder="Повторите пароль"
          :invalidText="invalidPasswordRepeatText"
        />
      </div>
    </div>   
    <hr class="form-block__line">
    <div class="form-block__toggle">  
      <ui-toggle 
        v-model="form.public"
        class="me-5"
      />
      <div class="form-block__toggle_info">
        Хотите чтобы Ваш профиль видели другие участники платформы?
        <span>
          Включает профиль для просмотра другими пользователями по ссылке
        </span>
      </div>
    </div>
    <div class="form-block__action">
      <div class="form-block__checkbox">
        <ui-checkbox 
          v-model="form.policy"
          class="me-14"
        />
        <div>
          Регистрируясь, Вы соглашаетесь с <a href="#">политикой конфиденциальности</a> и обработкой <a href="#">персональных данных</a> 
        </div>    
        <div 
          v-if="invalidPolicyText"
          class="form-block__checkbox_error"
        >
          {{ invalidPolicyText }}
        </div>  
      </div>
      <button class="btn form-block__btn">
        Зарегистрироваться
      </button>      
    </div>
    <div 
      v-if="success"
      class="form-block__success"
    >
      Регистрация успешно завершена
    </div>
  </form>
</template>

<script>
import UiInput from '@/components/UI/UiInput.vue'
import UiCheckbox from '@/components/UI/UiCheckbox.vue' 
import UiToggle from '@/components/UI/UiToggle.vue'
import UiSelect from "@/components/UI/UiSelect.vue"

export default {
  name: 'App',
  components: {
    UiInput,
    UiCheckbox,
    UiToggle,
    UiSelect
  },
  data() {
    return {
      form: {
        public: true,
        user_name: '',
        role: null,
        email: '',
        password: '',
        password_repeat: '',
        policy: true
      },
      touch: false,
      success: false,
      optionSelect: [
        {
          value: 0,
          name: 'Должность 0'
        },
        {
          value: 1,
          name: 'Должность 1'
        },
        {
          value: 2,
          name: 'Должность 2'
        }
      ]
    }
  },
  computed: {
    invalidUserNameText() {
      if (!this.form.user_name && this.touch) {
        return 'Поле не заполнено'
      }
      if (this.form.user_name.length < 3 && this.touch) {
        return 'Минимальное количество символов 3'
      }
      return ''
    },
    invalidPasswordText() {
      if (!this.form.password && this.touch) {
        return 'Поле не заполнено'
      }
      if (this.form.password.length < 6 && this.touch) {
        return 'Минимальное количество символов 6'
      }
      return ''
    },
    invalidEmailText() {
      if (!this.form.email && this.touch) {
        return 'Поле не заполнено'
      }
      if (!/^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/.test(this.form.email) && this.touch) {
        return 'Введите корректный email'
      }
      return ''
    },
    invalidSelectText() {
      if (!this.form.role && this.form.role !== 0 && this.touch) {
        return 'Выберите значение'
      }
      return ''
    },
    invalidPasswordRepeatText() {
      if (this.form.password_repeat !== this.form.password && this.touch) {
        return 'Пароль не совпадает'
      }
      return ''
    },
    invalidPolicyText() {
      if (!this.form.policy && this.touch) {
        return 'Вам необходимо дать согласие'
      }
      return ''
    },
    isValidForm() {
      return !this.invalidUserNameText && 
        !this.invalidPasswordText && 
        !this.invalidEmailText && 
        !this.invalidPasswordRepeatText && 
        !this.invalidPolicyText &&
        !this.invalidSelectText
    }
  },
  methods: {
    async onSubmit() {
      this.touch = true
      if (this.isValidForm) {
        console.log('onSubmit', this.form)
        this.success = true
        this.resetForm()
        setTimeout(() => {
          this.success = false
        }, 5000)
      }
    },
    resetForm() {
      this.form = {
        public: true,
        user_name: '',
        role: null,
        email: '',
        password: '',
        password_repeat: '',
        policy: true
      },
      this.touch = false
    }    
  }
}
</script>

<style lang="scss">
@import '@/assets/css/variables.scss';

.form-block {
  position: relative;
  overflow: hidden;
  border-radius: 15px;
  background: white;
  width: 100%;
  max-width: 960px;
  padding: 17px 15px 66px 31px;

  &__title {
    font-size: 19px;
    font-weight: 700;
    line-height: 27px; 
    letter-spacing: -0.066px;
  }

  &__line {
    background: $grey;
    margin: 17px 0 17px;
    stroke-width: 1px;
    width: calc(100% + 46px); // ширина + padding корневого элемента (15+31)
    margin-left: -31px;
  }

  &__subtitle {
    font-size: 16px;
    font-weight: 500;
    line-height: 19px; 
    margin-bottom: 34px;
  }

  &__row {
    display: flex;
    margin-left: -7px;
    margin-right: -7px;
    flex-wrap: wrap;
    margin-bottom: 30px;
  }

  &__col {
    display: flex;
    flex-direction: column;
    padding-left: 7px;
    padding-right: 7px;
    width: 50%;
  }

  &__toggle {
    display: flex;
    margin-top: 23px;
    margin-bottom: 30px;

    &_info {                 
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      font-size: 16px;
      font-weight: 500;
      line-height: 19px;

      span {
        color: $grey-1;
        font-size: 14px;
        font-weight: 400;
        letter-spacing: -0.021px; 
        margin-top: 10px;
      }
    }
  }

  &__action {
    display: flex;
  }

  &__checkbox {
    display: flex;
    align-items: start;
    font-size: 14px;
    font-weight: 400;
    line-height: 19px; 
    letter-spacing: -0.021px;
    margin-right: 16px;
    position: relative;

    a {
      color: $blue-1;
      cursor: pointer;
      text-decoration: none;
      transition: opacity .2s ease-in;

      &:hover {
        opacity: .7;
      }
    }

    &_error {      
      font-size: 12px;
      line-height: 1;
      color: red;
      position: absolute;
      bottom: -16px;
    }
  }

  &__btn {
    max-width: 302px;
    width: 100%;
  }

  &__success {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    font-size: 19px;
    font-weight: 700;
    line-height: 27px; 
    letter-spacing: -0.066px;

   }
}

.mt-auto {
  margin-top: auto;
}

.mb-31 {
  margin-bottom: 31px;
}

.me-14 {
  margin-right: 14px;
}

.me-5 {
  margin-right: 5px;
}
</style>
