<template>
  <div>
    
      <v-list dense>
        <v-list-item @click.stop="right = !right">
          <v-list-item-action>
            <v-icon>mdi-settings</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Settings</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-footer app>
        <span>Darsda</span>

        <v-spacer />

        <span>&copy; </span>
      </v-footer>
   
  </div>
</template>
<script>
export default {
  data: () => ({
    right: false,
    left: false,
  }),
};
</script>

<style scoped></style>
