<template>
  <v-timeline :dense="$vuetify.breakpoint.smAndDown" :width="'100%'">
    <v-timeline-item
      v-for="(seccion, i) in secciones"
      :key="i"
      :data-aos="`flip-${flip[Math.floor(Math.random() * 4)]}`"
      data-aos-delay="100"
      fill-dot
      :right="i % 2 != 0"
      :left="i % 2 == 0"
      :small="true"
    >
      <template v-slot:icon>
        <v-avatar>
          <img :src="seccion.ico || 'caslogo.png'" />
        </v-avatar>
      </template>
      <template v-slot:opposite>
        <a :href="seccion.link" target="_blank">
          <span
            :class="`white--text font-quicksand text-md-h5`"
            v-text="seccion.title"
          ></span>
        </a>
      </template>
      <v-hover v-slot:default="{ hover }">
        <v-card>
          <!--HOVER-->

          <v-expand-transition>
            <div
              v-if="hover"
              class="d-flex transition-fast-in-fast-out darken-2 v-card--reveal font-quicksand white--text text-justify"
              :class="seccion.color_card"
              style="height: 100%"
            >
              <div
                class="pr-9 pl-9"
                v-html="explicaciones[seccion.explicacion].content"
              ></div>
            </div>
          </v-expand-transition>
          <v-card-title :class="seccion.color_card">
            <img :src="seccion.icon_lead" alt="" width="50" class="mr-4" />
            <h2 class="white--text font-weight-light font-raleway">
              {{ seccion.titulo_lead_seccion }}
            </h2>
          </v-card-title>
          <v-container>
            <v-row>
              <v-col
                :cols="$vuetify.breakpoint.smAndDown ? 12 : 9"
                md="9"
                class="font-montalternates text-justify"
              >
                <div v-html="seccion.Texto"></div>
              </v-col>
              <v-col
                class="hidden-sm-and-down text-right d-flex justify-center align-center"
                md="3"
              >
                <img width="100px" :src="seccion.img" />
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-hover>
    </v-timeline-item>
  </v-timeline>
</template>

<script lang="ts">
declare interface window {
  onload(): void;
}
declare interface AOS {
  init(): void;
}
import seccionesJson from "@/static/secciones.json";
import explicaciones from "@/static/explicaciones.json";
import Swal from "sweetalert2";
import { Howl, Howler } from "howler";
import AOS from "aos";
import Vue from "vue";
export default Vue.extend({
  data() {
    return {
      secciones: seccionesJson.secciones,
      explicaciones: explicaciones.explicaciones,
      flip: ["left", "right", "down", "up"],
    };
  },
  mounted() {
    var sound = new Howl({
      src: ["castilla.mp3"],
      autoplay: false,
      loop: true,
      volume: 0.5,
      onend: function () {
        console.log("Finished!");
      },
      onplay: function () {
        console.log("Started");
      }
    });
Swal.fire(
  {
    icon:'question',
    title:"Linea de tiempo",
    html:"Bienvenido a linea de tiempo del lenguaje español",
    allowOutsideClick: false,
    
  }
).then((result) => {
  /* Read more about isConfirmed, isDenied below */
  if (result.isConfirmed) {
    sound.play();
  }
})
    AOS.init();
  },
});
</script>

<style>
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  position: absolute;
  width: 100%;
}
</style>
