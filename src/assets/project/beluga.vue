<script setup lang="ts">
import { nextTick, onMounted, ref } from "vue";
const vueRef = ref<any>(null);
const lights_mig35 = ref();
lights_mig35.value=[
  {
    type: "point",
    color: "#ffffff",
    position: { x: 0, y: 0, z: 500 },
    intensity: 0.25
  },
  {
    type: "DirectionalLight",
    position: { x: 100, y: 0, z: 0 },
    color: "",
    intensity: 0.75,
  },
  {
    type: "DirectionalLight",
    position: { x: -100, y: 0, z: 0 },
    color: "",
    intensity: 0.75,
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: 100, z: 0 },
    color: "",
    intensity: 0.35,
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: -100, z: 0 },
    color: "",
    intensity: 0.65,
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: 0, z: 100 },
    color: "",
    intensity: 0.35,
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: 0, z: -100 },
    color: "",
    intensity: 0.25,
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
    <div class="model" id="mig-35">
    <div class="">
      <vue3dLoader
      filePath="models/beluga/beluga.dae"
      :cameraPosition="{ x: 10, y: 5, z: 7}"
      ref="vueRef"
      :height="500"
      :backgroundColor="'#0a0a0a'"
      :lights="lights_mig35"
      :pointLightFollowCamera="true"
      :minDistance="7"
      :maxDistance="100"
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
      <p class="hero-title2">Airbus Beluga</p>
      <p class="aero-innovations-text-style-2">Airbus Beluga (Airbus A300-600ST, Super Transporter) — широкофюзеляжный реактивный грузовой самолёт компании Airbus для транспортировки крупногабаритных грузов. Имя Beluga происходит от формы корпуса самолёта, который напоминает кита-белуху (beluga в английском и некоторых других языках; не путать с белугой). Самолёт создан на базе типового широкофюзеляжного планера Airbus A300. Для перевозки агрегатов фюзеляж расширили до 7,1 м в диаметре, изменили переднюю часть, установили специальную систему, позволяющую откидывать кабину пилотов при загрузке грузов, усилили хвостовую часть для обеспечения устойчивости во время полётов. Производство лайнера началось в 1992 году, первый полёт состоялся в сентябре 1994 года. В эксплуатацию самолёт приняли в октябре 1995 года. Всего было построено 5 таких самолётов.</p>
      <p class="aero-innovations-text-style-2"><img src="/src/assets/user-svgrepo-com.svg" alt="" style="width: 25px; margin-bottom: 5px;"> Модель разработал: <b>Малозёмов Юрий</b></p>
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