<template>
  <div class="container">
    <TheHeader />
    <TheHome />
    <TheFooter />
  </div>
</template>

<script>
import TheFooter from '@/components/TheFooter.vue';
import TheHeader from '@/components/TheHeader.vue';
import TheHome from '@/pages/TheHome.vue';


export default {
  components: {
    TheHeader,
    TheFooter,
    TheHome
  }
}
</script>