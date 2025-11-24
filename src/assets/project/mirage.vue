<script setup lang="ts">
import { nextTick, onMounted, ref } from "vue";
const vueRef = ref<any>(null);
const lights_mirage = ref();
lights_mirage.value=[
  {
    type: "AmbientLight",
    color: "white",
    intensity: 1.75,
  },
  {
    type: "point",
    color: "#ffffff",
    position: { x: 0, y: 0, z: 500 },
    intensity: 0.25
  }
];

const currentModelIndex = ref();
const process = ref(0);
function onProcess(event: any, index: number) {
  process.value = Math.floor((event.loaded / event.total) * 100);
  if (index != 0) {
    currentModelIndex.value = index;
  }
};

const autoPlay = ref(true);
function change() {
  if (autoPlay.value) {
    autoPlay.value = false;
  } else {
    autoPlay.value = true;
  }
};
</script>

<template>
    <div class="model" id="mirage-2000">
    <div class="">
      <vue3dLoader
      filePath="models/mirage.fbx"
      :cameraPosition="{ x: 1000, y: 250, z: 700}"
      ref="vueRef"
      :height="500"
      :backgroundColor="'#0a0a0a'"
      :lights="lights_mirage"
      :pointLightFollowCamera="true"
      :minDistance="750"
      :maxDistance="3000"
      @process="onProcess"
      :autoPlay="autoPlay"
      :enableDamping="true"
      :dampingFactor="0.1"
      />

<div class="playpause" style="text-align: center; display: flex; justify-content: center;" v-if="process === 100">
      <div class="form-check form-switch">
        <input class="form-check-input" type="checkbox" role="switch" id="switchCheckChecked" @change="change()" checked>
        <label class="form-check-label" for="switchCheckChecked">Проигрывать анимацию</label>
    </div>
    </div>
    <div class="progressbar" v-if="process != 100" style="text-align: center;">
      <p style="color: white; margin-bottom: 7px;">Загрузка модели, пожалуйста подождите...</p>
    <div class="progress" role="progressbar" aria-label="Animated striped example" :aria-valuenow="process" aria-valuemin="0" aria-valuemax="100">
  <div class="progress-bar progress-bar-striped progress-bar-animated" :style="{width: process + '%'}">{{ process }}%</div>
  </div>
</div>

    </div>
    <div class="title-2">
      <p class="hero-title2">Dassault Mirage 2000</p>
      <p class="aero-innovations-text-style-2">Dassault Mirage 2000 — французский многоцелевой истребитель четвёртого поколения. Разработан в 1970-х годах фирмой «Дассо». На вооружении с 1984 года. Основной боевой самолёт ВВС Франции в конце XX — начале XXI века. Состоит на вооружении нескольких стран Азии, Европы и Латинской Америки.
Вооружён двумя пушками калибра 30 мм с боекомплектом в 125 снарядов на каждую. У самолёта девять точек подвески: пять — под фюзеляжем и четыре — под крылом. Может нести до четырёх ракет «воздух-земля», четыре-шесть ракет класса «воздух-воздух», четыре блока неуправляемых ракет, а также корректируемые или свободнопадающие бомбы.
Также самолёт может быть оснащён подвесными топливными баками для увеличения дальности полёта.
      </p>
      <p class="aero-innovations-text-style-2"><img src="/src/assets/user-svgrepo-com.svg" alt="" style="width: 25px; margin-bottom: 5px;"> Модель разработал: <b>Улыбин Егор</b></p>
    </div>
  </div>
</template>

<style>
.progressbar {
  margin-left: 35px;
  margin-right: 35px;
}
.title-2 {
  text-align: center;
  margin-left: 20px;
  margin-right: 20px;
}
.hero-title2 {
  font: 900 50px/75px Poppins, sans-serif;
  color: white;
  margin-bottom: 0px;
}
.aero-innovations-text-style-2 {
  font: 500 20px/35px Poppins, sans-serif;
  color: white;
  /* margin-right: 70px; */
  text-align: justify;
}
</style>