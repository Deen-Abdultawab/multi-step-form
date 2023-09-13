<template>
  <div class="sec">
    <FormWindow />
  </div>

</template>

<script>
import FormWindow from './components/FormWindow.vue'

export default {
  components: { FormWindow }
}

</script>

<style>
  .sec {
    width: 100%;
    background: var(--Light-blue);
    display: grid;
    min-height: 100vh;
    place-items: center;
  }

     @media only screen and (max-width: 600px){

        
        .sec {
            
            height: 100vh;
        }
    }
</style>
