<template>
  <div class="c-users">
    <div class="title">
      <h1>{{ title }}</h1>
      <div class="title__links">
        <a @click="resetUser">Сбросить</a>
        <a @click="updateUsers">Обновить</a>
      </div>
    </div>

    <div class="users clr">
      <!-- список пользователей -->
      <div class="users__list">
        <div v-if="loading">
          <ul v-if="users.length" class="list">
          <li v-for="user in users" :key="user.id">
            <b>Name:</b> <a @click="getUserById(user.id); addInCart(user)">{{ user.name }}</a>, <b>Username:</b> {{ user.username }}, <b>Email:</b> {{ user.email }}
          </li>
        </ul>
        </div>
        <div v-else>
          <div class="loading">Подождите идёт загрузка ...</div>
        </div>
      </div>
      <!-- подробная инфа по пользователю -->
      <div class="users__card">
        <div v-if="user.id">
          <pre>{{ user }}</pre>
        </div>
        <div v-else>
          <div class="loading">Пользователь не выбран</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Users',
  data: function () {
    return {
      url: 'https://jsonplaceholder.typicode.com',
      title: 'Пользователи',
      loading: false,
      users: [],
      user: {},
      cart: []
    }
  },
  methods: {
    getUsers: function () {
      this.$http.get(this.url + '/users').then(function (response) {
        console.log(response)
        this.users = response.body
        setTimeout(() => {
          this.loading = true
        }, 1000)
      }, function (error) {
        console.log(error)
        this.loading = true
      })
    },
    updateUsers: function () {
      this.loading = false
      this.users = []
      this.getUsers()
    },
    getUserById: function (userId) {
      this.users.some(user => {
        if (user.id === userId) {
          this.user = user
        }
      })
    },
    resetUser: function () {
      this.user = {}
    },
    addInCart: function (user) {
      console.log('Add user', user)
    }
  },
  created: function () {
    this.getUsers()
  }
}
</script>

<style lang="scss" scoped>
.title {
  padding: 2.5rem 0 1.5rem;
  & > h1 {
    border-bottom: 1px solid #dedede;
    margin: 0 0 1.5rem;
    padding-bottom: 1.5rem;
  }
  &__links {
    font-size: 1.3rem;
    & > a {
      margin-right: 1rem;
    }
  }
}

.users {
  & > div {
    float: left;
    width: 50%;
    & > div {
      padding: 0 1.5rem;
    }
  }
}

.list {
  & > li {
    font-size: 1.5rem;
    margin: 1.5rem 0;
  }
  & b {
    font-weight: bold;
  }
}

.loading {
  text-align: center;
  font-size: 1.3rem;
}
</style>
