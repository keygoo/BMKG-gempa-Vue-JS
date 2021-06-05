<template>
	<v-app-bar
      app
      color="deep-purple"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="EQalertID"
          class="shrink mr-2"
          contain
          src="../../assets/logo.png"
          transition="scale-transition"
          width="200"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/retorica-puzzle/BMKG-gempa-Vue-JS"
        target="_blank"
        text
      >
        <span class="mr-2">Versi Terbaru</span>
        <v-icon>mdi-github</v-icon>
      </v-btn>
    </v-app-bar>
</template>
<script>
	export default{
		name: 'Header',
	};
</script>