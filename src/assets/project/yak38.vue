<script setup lang="ts">
import { nextTick, onMounted, ref } from "vue";
const vueRef = ref<any>(null);
const lights_yak38 = ref();
lights_yak38.value=[
  {
    type: "AmbientLight",
    color: "white",
    intensity: 3.75,
  },
  {
    type: "point",
    color: "#ffffff",
    position: { x: 0, y: 0, z: -500 },
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
    <div class="model" id="su-30">
    <div class="">
      <vue3dLoader
      filePath="models/yak38.fbx"
      :cameraPosition="{ x: -1000, y: 500, z: -500 }"
      ref="vueRef"
      :height="500"
      :backgroundColor="'#0a0a0a'"
      :lights="lights_yak38"
      :pointLightFollowCamera="true"
      :minDistance="800"
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
      <p class="hero-title2">Як-38</p>
      <p class="aero-innovations-text-style-2">Як-38 (до 1976 года обозначался «Як-36М») — советский лёгкий палубный штурмовик, первый в СССР серийный самолёт вертикального взлёта и посадки.

Предназначался для поражения береговых объектов и кораблей водоизмещением до 4000–5000 т, для авиационной поддержки боевых действий сухопутных сил в тактической и ближайшей оперативной глубине расположения противника, для борьбы с самолётами ДРЛО, транспортными самолётами и вертолётами и для ведения визуальной разведки.

Самолёт был рассчитан для базирования на авианесущих крейсерах проекта 1143 («Киев», «Минск», «Новороссийск», «Баку»).

Всего был построен 231 самолёт Як-38 различных модификаций в 1974–1989 годах. Серийный выпуск машины осуществлялся на Саратовском авиазаводе.</p>
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