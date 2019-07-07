<template>
  <v-app>
    <v-content>
      <Speaker/>
    </v-content>
  </v-app>
</template>

<script lang="ts">
    import { Vue, Component } from 'vue-property-decorator'
    import Speaker from './components/Speaker.vue'

    @Component({
        components: {
            Speaker
        }
    })
    export default class App extends Vue {
    }
</script>
