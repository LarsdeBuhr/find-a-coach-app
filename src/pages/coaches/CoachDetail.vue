<template>
<fragment>

   <section>
      <base-card>
      <h2>{{fullName}}</h2>
      <h3>${{rate}}/hour</h3>
      </base-card>
   </section>

<section>
   <base-card>
   <header>
   <h2>Interested? Reach out now!</h2>
   <base-butto link :to="contactLink">Contact</base-butto></header>
   <router-view></router-view>
   </base-card>
</section>

<section>
   <base-card>
      <base-badge v-for="area in areas" :key="area" :type="area" :title="area">
      <p>{{description}}</p>
      </base-badge>
   </base-card>
</section>

</fragment>
</template>

<script>
export default {
   props:["id"],
   data(){
      return{
         selectedCoach: null
      }
   },
   created(){
      this.selectedCoach = this.$store.getters["coaches/coaches"].find(coach => coach.id === this.id);
   },
   computed:{
      areas(){
         return this.selectedCoach.areas;
      },
      rate(){
         return this.selectedCoach.hourlyRate;
      },
      description(){
         return this.selectedCoach.description;
      },
      fullName(){
         return this.selectedCoach.firstName + " " + this.selectedCoach.lastName;
      },
      contactLink(){
         return this.$route.path + "/" + this.id + "/contact";
      }
   }
};
</script>

<style></style>
