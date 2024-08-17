<script setup lang="ts">
import SideBar from '@/components/SideBar.vue';
import { getUser } from '@/services/api';
import { onMounted, ref } from 'vue';
import type { UserType } from '@/types';
import { tempoDesdeCriacao } from '@/utils/PastTime';
import ExploreComponent from '@/components/ExploreComponent.vue';
import { items } from '@/utils/ExploreArray';
import ApplicationBar from '@/components/ApplicationBar.vue';

const item = ref<any>();

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
});
</script>
<template>
  <v-row class="ma-0 pa-0">
    <v-col cols="3" class="d-none d-md-flex">
      <SideBar :item="item" />
    </v-col>
    <v-col cols="12" md="6">
      <span class="home-content-title">
        <span> Explorar </span>
      </span>

      <div class="explore-div" v-for="(item, index) in items" :key="index">
        <p>{{ item.title }} - {{ tempoDesdeCriacao(item.created_at) }}</p>
        <h4>{{ item.content }}</h4>
      </div>
    </v-col>
    <v-col cols="3" class="d-none d-md-flex">
      <ExploreComponent />
    </v-col>
  </v-row>
  <ApplicationBar class="d-flex d-md-none" />
</template>

<style scoped>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

.explore-div {
  margin: 1rem;
  margin-bottom: 1.6rem;
}

.explore-div p {
  font-size: 0.8rem;
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
