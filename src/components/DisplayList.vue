<template>
    <div>
        <div v-if="loading">
            ...LOADING
        </div>
        <ul id="list" v-if="!loading">
            <li
            v-for="user in users"
            :key="user.id.value">
                {{ user.name.first }}
            </li>
        </ul>
    </div>
</template>

<script>
import { FETCH_USERS_URL } from '../constants/ApiConstants';

export default {
    name:'DisplayList',
    data: function(){
        return {
            loading: true,
            users: []
        }
    },
    created() {
    this.fetchFacts();
    },
    methods: {
    fetchFacts() {
      fetch(FETCH_USERS_URL)
        .then(resp => resp.json())
        .then(data => {
            this.users = data.results
            this.loading = false;
            });
    }
  }
}
</script>

<style>
#list {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: medium;
  list-style-type:none;
}
</style>
