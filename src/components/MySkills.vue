<script>
import { SplideSlide } from "@splidejs/vue-splide";
import Splide from "@splidejs/splide";
import { AutoScroll } from "@splidejs/splide-extension-auto-scroll";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/all";
gsap.registerPlugin(ScrollTrigger);

export default {
  name: "MySkills",
  components: {
    Splide,
    SplideSlide,
  },
  data() {
    return {
      technologies: [
        {
          name: "VueJS",
          image: "vue.svg",
        },
        {
          name: "JS",
          image: "javascript.svg",
        },

        {
          name: "Laravel",
          image: "laravel.svg",
        },

        {
          name: "HTML",
          image: "html.svg",
        },

        {
          name: "Bootstrap",
          image: "bootstrap.svg",
        },

        {
          name: "CSS",
          image: "css.svg",
        },

        {
          name: "PHP",
          image: "php.svg",
        },

        {
          name: "Sass",
          image: "sass.svg",
        },

        /* sql: {
          name: "sql",
          image: "sql.svg",
        }, */

        {
          name: "Vite",
          image: "vite.svg",
        },

        {
          name: "Git",
          image: "git.svg",
        },
      ],
    };
  },

  methods: {
    slider() {
      const splide = new Splide(".splide", {
        type: "loop",
        drag: "free",
        focus: "center",
        perPage: 6,
        arrows: false,
        pagination: false,
        autoScroll: {
          speed: 1,
          pauseOnHover: false,
        },
      });

      splide.mount({ AutoScroll });
    },

    animateHeading() {
      const text = document.querySelector(".skills-heading");

      gsap.from(text, {
        x: -1000,
        scale: 0.1,
        scrollTrigger: {
          trigger: text,
          start: "top 85%",
          end: "bottom 20%",
          scrub: true,
          pin: true,
        },
      });
    },
  },
  mounted() {
    this.slider();
    this.animateHeading();
  },
};
</script>
<template>
  <section id="skills">
    <h1 class="md-container skills-heading">Skills</h1>
    <div class="splide skills-slider" aria-label="skills">
      <div class="splide__track">
        <ul class="splide__list align-center">
          <splide-slide v-for="tech in technologies">
            <img
              class="tech"
              width="100"
              :src="`/public/img/${tech.image}`"
              :alt="tech.tech"
            />
          </splide-slide>
        </ul>
      </div>
    </div>
  </section>
</template>
<style scoped>
@import "@splidejs/splide/dist/css/splide.min.css";
</style>
