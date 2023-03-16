<!-- <template>
    <div> -->
        <!-- Sign up page -->
       
    <!--</div>
</template>

<script setup>

// HomeView.vue
</script> REMOVE 3 X --> <!-- --> <!-- TO LEAVE WHAT WAS HERE ORIGINALLY -->

<script setup>
  import UserForm from "@/components/UserForm.vue"

  function login(user){
    //api request
    

  }
</script>

<template>
    <div>

      <UserForm formType="signin" @submit="login" />
      <!-- Login page -->
    </div>
    
</template>
