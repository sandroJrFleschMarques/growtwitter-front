<script setup lang="ts">
import SideBar from '@/components/SideBar.vue';
import ListCard from '@/components/ListCard.vue';
import { getUser, showPosts } from '@/services/api';
import type { TweetType } from '@/types/TweetType';
import { onMounted, ref } from 'vue';
import type { UserType } from '@/types';
import SpinnerComponent from '@/components/SpinnerComponent.vue';
import ExploreComponent from '@/components/ExploreComponent.vue';
import ApplicationBar from '@/components/ApplicationBar.vue';

const listenEmit = () => {
  fetchTweets();
};

const loadingVisible = ref<boolean>(false);
const tweets = ref<TweetType[]>([]);
const item = ref<UserType>();
const endpoint = '/posts';

async function fetchTweets() {
  loadingVisible.value = true;

  const response = await showPosts(endpoint);

  loadingVisible.value = false;

  tweets.value = response.data.data;
}

async function handleGetUser() {
  const userData = localStorage.getItem('userData');
  if (!userData) {
    const response = await getUser();
    item.value = response.data.data;
    localStorage.setItem('userData', JSON.stringify(item.value));
    return;
  }
  item.value = JSON.parse(userData);
}

onMounted(() => {
  handleGetUser();
  fetchTweets();
});
</script>

<template>
  <v-row class="ma-0 pa-0">
    <v-col cols="3" class="d-none d-md-flex" v-if="item">
      <SideBar :item="item" @call-emit="listenEmit" />
    </v-col>
    <v-col cols="12" md="6">
      <span class="home-content-title">
        <span> Página Inicial </span>
      </span>
      <ListCard :tweets="tweets" />
    </v-col>
    <v-col cols="3" class="d-none d-md-flex">
      <ExploreComponent />
    </v-col>
  </v-row>
  <div class="spinner-div d-flex justify-center mt-5">
    <SpinnerComponent v-if="loadingVisible" color="blue" />
  </div>
  <ApplicationBar class="d-flex d-md-none" @call-emit="listenEmit" />
</template>

<style scoped>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
.spinner-div {
  position: absolute;
  left: 46%;
  top: 50%;
}
.home-content-title {
  display: flex;
  align-items: center;
  padding: 1rem;
  width: 100%;
  height: 4rem;
  border-bottom: 2px solid #e9e9e9;
  font-weight: 600;
  font-size: 1.3rem;
  font-style: normal;
}
</style>
