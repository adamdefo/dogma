<template>
    <div class="b-auth">
        <div class="form-wrapper">
            <form @submit.prevent="logIn" class="form">
                <div class="form__group">
                    <div class="form__item">
                        <input id="login" v-model="login" class="control" type="text" name="login" />
                        <label class="label">Логин</label>
                    </div>
                    <div class="form__item">
                        <input id="pswd" v-model="pswd" class="control" type="password" name="pswd" />
                        <label class="label">Пароль</label>
                    </div>
                </div>

                <div class="form__item form__item--btn">
                    <button @click="logIn" class="btn" type="button" v-bind:disabled="!isValid">
                        <span>Войти</span>
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Auth',
  props: {},
  model: {
    login: {
      type: String,
      default: ''
    },
    pswd: {
      type: String,
      default: ''
    }
  },
  data: function () {
    return {
      count: 0,
      login: 'login',
      pswd: '',
      someData: ''
    }
  },
  methods: {
    checkUser: function () {
      console.log('Проверяю пользователя')
    },
    logIn: (event) => {
      let url = 'https://jsonplaceholder.typicode.com'
      console.log(this.login)

      this.$http.get(url + '/posts/1').then(response => {
        this.someData = response.body
        console.log(response.body)
      }, response => {
        console.log('error')
      })
    }
  },
  beforeCreate: function () {},
  created: function () {
    this.checkUser()
    this.count += 3
    console.log('created', this.count)
  },
  computed: {
    isValid: function () {
      return (this.login !== '') && (this.pswd !== '')
    }
  }
}
</script>

<style lang="scss" scoped>
.code {
  width: 600px;
  margin: 0 auto;
}

.b-auth {
  position: relative;
  width: 100%;
}

.form {
  position: relative;
  width: 100%;
  &-wrapper {
    position: relative;
    margin: 5rem auto;
    padding: 3rem;
    width: 100%;
    min-width: 300px;
    max-width: 400px;
  }
  &__group {
    position: relative;
    padding: 15px 0;
  }
  &__item {
    position: relative;
    padding: 15px 0;
    &--btn {
      padding: 0;
    }
    & > .label {
      position: absolute;
      top: 0;
      left: 0;
      color: #8f8f8f;
      font-size: 1.5rem;
    }
    & > .control {
      border: 1px solid #e8e8e8;
      -webkit-box-shadow: inset 1px 1px 0 rgba(0,0,0,.3);
      box-shadow: inset 1px 1px 0 rgba(0,0,0,.3);
      line-height: 30px;
      height: 30px;
      background: #fff;
      font-size: 1.5rem;
      color: #555e6c;
      padding: 5px;
      width: 100%;
      &:focus + label {
        display: none;
      }
    }
  }
}

.btn {
  cursor: pointer;
  font-size: 1.5rem;
  padding: 3px 6px;
}
</style>