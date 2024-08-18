<script setup lang="ts">
import homePageLogo from '@/components/icons/homePageLogo.vue';
import HashTagLogo from '@/components/icons/hashTagLogo.vue';
import ProfileLogo from '@/components/icons/profileLogo.vue';
import HomePageLogo from '@/components/icons/homePageLogo.vue';
import ButtonTweet from './ButtonTweet.vue';
</script>

<template>
  <v-layout>
    <v-bottom-navigation grow class="d-flex d-lg-none">
      <v-row>
        <v-col cols="3" class="d-flex d-lg-none">
          <v-btn>
            <RouterLink to="/"><HomePageLogo class="img-icon" /></RouterLink>
          </v-btn>
        </v-col>
        <v-col cols="3" class="d-flex d-lg-none">
          <v-btn>
            <RouterLink to="/explore"><HashTagLogo class="img-icon" /></RouterLink>
          </v-btn>
        </v-col>
        <v-col cols="3" class="d-flex d-lg-none">
          <v-btn>
            <RouterLink to="/profile"><ProfileLogo class="img-icon" /></RouterLink>
          </v-btn>
        </v-col>
        <v-col cols="3" class="d-flex d-lg-none">
          <v-btn>
            <ButtonTweet class="bg-white" />
          </v-btn>
        </v-col>
      </v-row>
    </v-bottom-navigation>
  </v-layout>
</template>

<style scoped>
.img-icon {
  max-width: 16vh;
  max-height: 25vh;
}
</style>
