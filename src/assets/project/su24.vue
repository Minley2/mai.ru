<script setup lang="ts">
import { nextTick, onMounted, ref } from "vue";
const vueRef = ref<any>(null);
const lights_mig35 = ref();
lights_mig35.value=[
  {
    type: "AmbientLight",
    color: "white",
    intensity: 0.7,
  },
  {
    type: "point",
    color: "#ffffff",
    position: { x: 0, y: 0, z: 500 },
    intensity: 0.3
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: 100, z: 100 },
    color: "",
    intensity: 0.25,
  }
];

const currentModelIndex = ref();
const process = ref(0);
function onProcess(event: any, index: number) {
  process.value = Math.floor((((event.loaded / event.total) * 100)/352)*100);
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
    <div class="model" id="mig-35">
    <div class="">
      <vue3dLoader
      filePath="models/su24.glb"
      :cameraPosition="{ x: 15, y: 5, z: 15}"
      ref="vueRef"
      :height="500"
      :backgroundColor="'#0a0a0a'"
      :lights="lights_mig35"
      :pointLightFollowCamera="true"
      :minDistance="13"
      :maxDistance="75"
      @process="onProcess"
      :autoPlay="autoPlay"
      :enableDamping="true"
      :dampingFactor="0.1"
      outputEncoding="sRGB"
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
      <p class="hero-title2">Су-24</p>
      <div class="video-container">
        <iframe width="720" height="405" src="https://rutube.ru/play/embed/4650bae3a84849280778b1fddfe909d2" frameBorder="0" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
      </div>
      <div class="content">
        <p class="aero-innovations-text-style-2">Су-24 (по кодификации НАТО — Fencer, с англ. «фехтовальщик») — советский и российский тактический фронтовой бомбардировщик с крылом изменяемой стреловидности. Предназначен для нанесения ракетно-бомбовых ударов по наземным и надводным целям, в том числе на малых высотах. 4 февраля 1975 года самолёт был принят на вооружение ВВС СССР под обозначением Су-24. Су-24 использовался в различных вооружённых конфликтах, включая Афганскую войну, обе чеченские войны, конфликт в Южной Осетии в 2008 году. 31 августа 2016 года в ВКС России завершилась эксплуатация бомбардировщиков Су-24 в исходном варианте, самолёты были сняты с вооружения.</p>
      </div>
      <p class="aero-innovations-text-style-2"><img src="/src/assets/user-svgrepo-com.svg" alt="" style="width: 25px; margin-bottom: 5px;"> Модель разработал: <b>Улыбин Егор</b></p>
    </div>
  </div>
</template>

<style>
  .video-container {
    float: right;
    margin: 10px 0 10px 20px;
    max-width: 50%;
  }

  .video-container iframe {
    width: 100%;
    height: 300px;
    aspect-ratio: 16 / 9;
  }

  .content {
    text-align: justify;
  }

  @media (max-width: 767px) {
    .video-container {
      float: none;
      margin: 5px auto 10px auto;
      max-width: 100%;
      width: 100%;
    }
    
    .video-container iframe {
      width: 100%;
      height: auto;
    }
  }
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