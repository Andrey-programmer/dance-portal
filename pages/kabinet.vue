<template>
  <div>
    <h2>Профиль</h2>
    <v-row>
      <v-col>
        <el-profile-card></el-profile-card>
      </v-col>
      <v-col></v-col>
      <v-col></v-col>
      <v-col></v-col>
    </v-row>
    <v-row>
      <v-col>
        <el-profile-main></el-profile-main>
      </v-col>
      <v-col>
        <el-profile-anketa></el-profile-anketa>
      </v-col>
      <v-col></v-col>
      <v-col></v-col>
    </v-row>
  </div>
</template>

<script>
  import profileCard from '@/components/profile/profile-card'
  import profileMain from '@/components/profile/profile-main'
  import profileAnketa from '@/components/profile/profile-anketa'
  export default {
    components: {
      elProfileCard: profileCard,
      elProfileMain: profileMain,
      elProfileAnketa: profileAnketa
    }
  }
</script>

<style scoped>

</style>
