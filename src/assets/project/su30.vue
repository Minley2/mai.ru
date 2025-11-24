<script setup lang="ts">
import { nextTick, onMounted, ref } from "vue";
const vueRef = ref<any>(null);
const lights_su30 = ref();
lights_su30.value=[
  {
    type: "AmbientLight",
    color: "white",
    intensity: 1.2,
  },
  {
    type: "point",
    color: "#ffffff",
    position: { x: 0, y: 0, z: 500 },
    intensity: 0.2
  }];

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
    <div class="model" id="su-30">
    <div class="">
      <vue3dLoader
      filePath="models/su30.fbx"
      :cameraPosition="{ x: 1250, y: 750, z: 750}"
      ref="vueRef"
      :height="500"
      :backgroundColor="'#0a0a0a'"
      :lights="lights_su30"
      :pointLightFollowCamera="true"
      :minDistance="1200"
      :maxDistance="5000"
      @process="onProcess"
      :autoPlay="autoPlay"
      :enableDamping="true"
      :dampingFactor="0.1"
      />
    </div>
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

    <div class="title-2">
      <p class="hero-title2">Су-30</p>
      <p class="aero-innovations-text-style-2">Су-30 — советский и российский двухместный многоцелевой истребитель поколения 4+. Предназначен для уничтожения воздушных целей в простых и сложных метеорологических условиях, блокирования вражеских аэродромов и управления групповыми боевыми действиями при завоевании господства в воздухе.
Разработка самолёта началась в 1988 году на базе Конструкторского бюро Сухого. Основой для Су-30 послужил учебно-боевой истребитель Су-27. Работы велись на Иркутском производственном объединении и завершились в 1992 году.
Су-30 предполагает наличие двух пилотов, что вместе с новой системой управления истребителями в группе позволяло более эффективно использовать сразу несколько самолётов. Кроме того, истребитель оснащён системой дозаправки в воздухе.</p>
      <p class="aero-innovations-text-style-2"><img src="/src/assets/user-svgrepo-com.svg" alt="" style="width: 25px; margin-bottom: 5px;"> Модель разработал: <b>Каюмов Матвей</b></p>
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