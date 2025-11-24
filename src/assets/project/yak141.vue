<script setup lang="ts">
import { nextTick, onMounted, ref } from "vue";
const vueRef = ref<any>(null);
const lights_mig35 = ref();
lights_mig35.value=[
  {
    type: "AmbientLight",
    color: "white",
    intensity: 1.25,
  },
  {
    type: "point",
    color: "#ffffff",
    position: { x: 0, y: 0, z: 500 },
    intensity: 0.25
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
    <div class="model" id="yak-141">
    <div class="">
      <vue3dLoader
      filePath="models/yak141.fbx"
      :cameraPosition="{ x: 1250, y: 350, z: 1250}"
      ref="vueRef"
      :height="500"
      :backgroundColor="'#0a0a0a'"
      :lights="lights_mig35"
      :pointLightFollowCamera="true"
      :minDistance="1000"
      :maxDistance="10000"
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
      <p class="hero-title2">Як-141</p>
      <p class="aero-innovations-text-style-2">Як-141 (внутреннее обозначение: изделие 48/48М) — многоцелевой сверхзвуковой всепогодный палубный истребитель вертикального/короткого взлёта и посадки разработки ОКБ Яковлева. Самолёт предназначался для обеспечения прикрытия авианосных соединений от авиации противника, завоевания и удержания господства в воздухе, ведения ближнего манёвренного и дальнего боя, а также для нанесения ударов по наземным и надводным целям. Первый полёт самолёта состоялся в 1987 году. Проект закрыт в 1992 году из-за кризиса, аварии с одним из опытных образцов и негативного отношения военных к «вертикалкам». Оба лётных образца Як-141 сохранились и являются экспонатами музеев.</p>
      <p class="aero-innovations-text-style-2"><img src="/src/assets/user-svgrepo-com.svg" alt="" style="width: 25px; margin-bottom: 5px;"> Модель разработал: <b>Овчинников Алексей</b></p>
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