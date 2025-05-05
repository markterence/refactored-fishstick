<template>
  <div>
    <Logo />

    <h1>Welcome to Nuxt Application</h1>

    <p>
    {{ jsonData }}
    </p>
  </div>
</template>

<script lang="ts" setup>
import axios from 'axios';

const jsonData = ref();
 

onMounted(async () => {
  try {

    console.log('onMounted')
    const { data: res } = await axios.get('https://get.geojs.io/v1/ip/geo.json');
    const { country, country_code, timezone }: { country: string; country_code: string; timezone: string } = res;
    const data = { country, country_code, timezone };

    jsonData.value = data;
    
    console.log('jsonData', jsonData.value);

  } catch (error) {
    console.log('error', error)
  }
})
</script>