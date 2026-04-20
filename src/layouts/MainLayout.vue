<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          <div class="text-weight-light text-uppercase">
            {{ projectName }}
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>
    <q-footer ckass="bg-blue-10" elevated>
      <q-toolbar>
        <q-toolbar-title>
          <div
            class="row text-uppercase justify-between text-overline text-weight-light"
          >
            <div>Powered by the Filmore</div>
            <div>Copyright &copy; {{ currentYear }}</div>
            <div>
              {{ projectShortName }}
              {{ projectVersion }}
            </div>
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
    <q-drawer elevated v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header class="text-overline text-uppercase text-center">
          {{ projectName }}
        </q-item-label>
        <EssentialLink
          v-for="link in navLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";
import { mapGetters } from "vuex";

export default defineComponent({
  name: "MainLayout",
  components: {
    EssentialLink,
  },
  data() {
    return {
      leftDrawerOpen: false,
    };
  },
  methods: {
    toggleLeftDrawer() {
      this.leftDrawerOpen = !this.leftDrawerOpen;
    },
  },
  computed: {
    projectName() {
      return process.env.PROJECT_NAME;
    },
    projectShortName() {
      return process.env.PROJECT_SHORT_NAME;
    },
    projectVersion() {
      return process.env.PROJECT_VERSION;
    },
    currentYear() {
      return new Date().getFullYear();
    },
    ...mapGetters({
      navLinks: "helpers/navLinks",
    }),
  },
});
</script>
