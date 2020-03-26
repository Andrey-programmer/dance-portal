<template>
   <v-card
        class="mx-auto"
        max-width="344"
        outlined
      >
        <v-list-item three-line>
          <v-list-item-avatar
            tile
            size="100"
            color="grey"
          ></v-list-item-avatar>
          <v-list-item-content>
            <div class="overline mb-4">Андрей</div>
            <v-list-item-title class="headline mb-1">Ловец Снов</v-list-item-title>
            <v-list-item-subtitle>Слоган</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <v-card-actions>
          <v-tooltip bottom>
            <template v-slot:activator="{ on }">
              <v-btn
                class="mx-2"
                fab
                dark
                color="indigo"
                v-on="on"
              >
                <v-icon dark>mdi-plus</v-icon>
              </v-btn>
            </template>
            <span>Аватар</span>
          </v-tooltip>
          <v-btn text>Button</v-btn>
        </v-card-actions>
      </v-card>
</template>

<script>
  export default {

  }
</script>

<style scoped>

</style>
