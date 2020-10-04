<template>
  <div class="container">
    <header class="jumbotron">
      <h3>Страница списка всех пользователей</h3>
    </header>
    <div>
      <ul>
        <li v-for="user in content" :key="user.id">
          <p>Пользователь №{{user.id}}</p>
          <p>Имя пользователя: {{user.username}}</p>
          <p>Логин: {{user.login}}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import UserService from '../services/user.service';

export default {
  name: 'User',
  data() {
    return {
      content: ''
    };
  },
  mounted() {
    UserService.getUserBoard().then(
        response => {
          this.content = response.data;
        },
        error => {
          this.content =
              (error.response && error.response.data) ||
              error.message ||
              error.toString();
        }
    );
  }
};
</script>
