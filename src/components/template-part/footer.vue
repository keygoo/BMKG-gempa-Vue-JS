<template>
 <v-footer
    dark
    padless
    justify="center"
  >
    <v-card
      class="flex"
      flat
      tile 
    >
      <v-card-title class="teal">
        <strong class="subheading">Data bersumber dari <a href="https://data.bmkg.go.id/gempabumi/" target="new" class="linkbmkg">Badan Meteorologi, Klimatologi, dan Geofisika (BMKG)</a></strong>

        <v-spacer></v-spacer>
        <a href="https://www.bmkg.go.id/" target="new">
        <v-btn
          v-for="icon in icons"
          :key="icon"
          class="mx-4"
          dark
          icon
        >
          <v-icon size="24px">
           {{icon}}
          </v-icon>
        </v-btn>
        </a>
      </v-card-title>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} &copy; <strong>Retorica-Puzzle</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>
<script>
export default{
  name: 'Footer',
  data: () => ({
      icons: [
        'mdi-web',
      ],
    }),
};
</script>
<style scope>
.linkbmkg{
  color: #ffffff !important;
  text-decoration: none;
}
</style>