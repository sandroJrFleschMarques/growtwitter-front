<script setup lang="ts">
import HashTagLogo from '@/components/icons/hashTagLogo.vue';
import ProfileLogo from '@/components/icons/profileLogo.vue';
import HomePageLogo from '@/components/icons/homePageLogo.vue';
import ButtonTweet from './ButtonTweet.vue';
import { logout } from '@/services/api';
import router from '@/router';
import { resetStorage } from '@/services/authentication';

async function handlogout() {
  const response = await logout();
  if (response.status === 200) {
    resetStorage();
    router.push('/login');
  } else if (response.status === 400) {
    alert('Falha ao deslogar.');
  } else {
    alert('Ocorreu um erro entre em contato com o suporte.');
  }
}
</script>

<template>
  <v-layout>
    <v-bottom-navigation grow class="d-flex d-lg-none">
      <v-row>
        <v-col cols="3" class="d-flex justify-center d-lg-none col-blue">
          <v-btn>
            <ButtonDefault class="" @click="handlogout"
              ><span class="mdi mdi-exit-to-app"></span
            ></ButtonDefault>
          </v-btn>
        </v-col>
        <v-col cols="2" class="d-flex justify-center d-lg-none col-black">
          <v-btn>
            <RouterLink to="/"><span class="mdi mdi-home"></span></RouterLink>
          </v-btn>
        </v-col>
        <v-col cols="2" class="d-flex justify-center d-lg-none col-black">
          <v-btn>
            <RouterLink to="/explore"><span class="mdi mdi-pound"></span></RouterLink>
          </v-btn>
        </v-col>
        <v-col cols="2" class="d-flex justify-center d-lg-none col-black">
          <v-btn>
            <RouterLink to="/profile"><span class="mdi mdi-account-outline"></span></RouterLink>
          </v-btn>
        </v-col>
        <v-col cols="3" class="d-flex justify-center d-lg-none">
          <v-btn>
            <ButtonTweet class="col-blue" />
          </v-btn>
        </v-col>
      </v-row>
    </v-bottom-navigation>
  </v-layout>
</template>

<style scoped>
.mdi {
  max-width: 16vh;
  max-height: 25vh;
}
@media (max-width: 959px) {
  .col-black {
    color: black !important;
  }

  .col-blue,
  v-btn--variant-flat {
    color: rgb(66, 133, 244) !important;
  }
}
</style>
