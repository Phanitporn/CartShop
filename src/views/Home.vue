Home
<template>
  <div class="Shop">
    <div>
  <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand href="">PRODUCTS</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      
      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
       
         
        

       
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>

    <h1 class="my-4" style="color:indigo">PRODUCTS</h1>
    <Cart />
  </div>
</template>

<script>
// @ is an alias to /src
import Cart from "@/components/Cart.vue";

export default {
  name: "Shop",
  components: {
    Cart
  }
};
</script>\
<style  >

</style>>
  
