<script setup lang="ts">
import { nextTick, onMounted, ref } from "vue";
const vueRef = ref<any>(null);
const lights_lancet = ref();
lights_lancet.value=[
  {
    type: "AmbientLight",
    color: "white",
    intensity: 0.8,
  },
  {
    type: "point",
    color: "#ffffff",
    position: { x: 0, y: 0, z: 500 },
    intensity: 0.2
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
    <div class="model" id="su-25">
        <div class="">
        <vue3dLoader
        filePath="models/lancet-1.fbx"
        :cameraPosition="{ x: 1700, y: 750, z: 1000}"
        ref="vueRef"
        :height="500"
        :backgroundColor="'#0a0a0a'"
        :lights="lights_lancet"
        :pointLightFollowCamera="true"
        :minDistance="1000"
        :maxDistance="3000"
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
        <p class="hero-title2">БПЛА «Ланцет»</p>
        <p class="aero-innovations-text-style-2">
            БПЛА «Ланцет» — это беспилотный барражирующий боеприпас, разработанный российской компанией ZALA. Он предназначен для поражения наземной техники и других важных целей на переднем крае и в ближнем тылу противника. « Ланцет» может использоваться как для ударных, так и для разведывательных задач. Он оснащён интеллектуальными, навигационными и коммуникационными модулями, а также приборами оптико-электронного и телевизионного наведения. « Ланцет» имеет видеокамеры в инфракрасном и видимом диапазоне, наведение на лазерный целеуказатель, а также датчик поиска целей газоанализатором и радиометром.</p>
        <p class="aero-innovations-text-style-2"><img src="/src/assets/user-svgrepo-com.svg" alt="" style="width: 25px; margin-bottom: 5px;"> Модель разработали: <b>Минайлов Пётр, Каюмов Матвей</b></p>
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