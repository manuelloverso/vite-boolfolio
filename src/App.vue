<script>
// IMPORTS
import { store } from "./store";
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import ProjectCard from "./components/ProjectCard.vue";
import lenis from "./lenis";
import CustomCursor from "./components/CustomCursor.vue";
export default {
  name: "App",
  components: {
    AppHeader,
    AppFooter,
    ProjectCard,
    CustomCursor,
  },
  data() {
    return {
      store,
      backgroundUpdate: "",
    };
  },

  watch: {
    $route: {
      handler: "handleBackground",
      immediate: true,
    },
  },

  methods: {
    handleBackground() {
      setTimeout(() => {
        if (this.$route.name == "contacts") {
          this.backgroundUpdate = "bg-contacts";
        } else if (
          this.$route.name == "projects" ||
          this.$route.name == "ProjectShow"
        ) {
          this.backgroundUpdate = "bg-projects";
        } else {
          this.backgroundUpdate = "";
        }
      }, 1000);
    },
  },

  mounted() {
    store.isTouch = store.isTouchDevice();

    /* scroll */
    lenis.on("scroll", (e) => {});

    function raf(time) {
      lenis.raf(time);
      requestAnimationFrame(raf);
    }

    requestAnimationFrame(raf);
  },
};
</script>
<template>
  <template v-if="!store.isTouch">
    <!-- custom cursor -->
    <CustomCursor />
  </template>

  <div ref="bg-1" class="bg-bobble1 bobble" :class="backgroundUpdate"></div>
  <div ref="bg-2" class="bg-bobble2 bobble" :class="backgroundUpdate"></div>
  <!-- Site Header -->
  <AppHeader />

  <RouterView v-slot="{ Component }">
    <transition name="slide-fade" mode="out-in">
      <component :is="Component" :key="$route.path" />
    </transition>
  </RouterView>

  <!-- Site Footer -->
  <AppFooter />
</template>
<style>
/* background */

.bg-projects {
  background-color: rgb(186, 22, 22) !important;
}

.bg-contacts {
  background-color: rgb(6, 79, 10) !important;
}

.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
.mf-cursor::before {
  background: rgb(197, 205, 209);
  transform: scale(0.4);
}

.mf-cursor-text {
  color: black;
}
</style>
