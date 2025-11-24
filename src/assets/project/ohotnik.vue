<script setup lang="ts">
import { nextTick, onMounted, ref } from "vue";
const vueRef = ref<any>(null);
const lights_mig35 = ref();
lights_mig35.value=[
  {
    type: "point",
    color: "#ffffff",
    position: { x: 0, y: 0, z: 500 },
    intensity: 10
  },
  {
    type: "DirectionalLight",
    position: { x: 100, y: 0, z: 0 },
    color: "",
    intensity: 10,
  },
  {
    type: "DirectionalLight",
    position: { x: -100, y: 0, z: 0 },
    color: "",
    intensity: 10,
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: 100, z: 0 },
    color: "",
    intensity: 10,
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: -100, z: 0 },
    color: "",
    intensity: 10,
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: 0, z: 100 },
    color: "",
    intensity: 10,
  },
  {
    type: "DirectionalLight",
    position: { x: 0, y: 0, z: -100 },
    color: "",
    intensity: 10,
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
      filePath="models/ohotnik/ohotnik.dae"
      :cameraPosition="{ x: -10, y: 5, z: -10}"
      ref="vueRef"
      :height="500"
      :backgroundColor="'#0a0a0a'"
      :lights="lights_mig35"
      :pointLightFollowCamera="true"
      :minDistance="9"
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
      <p class="hero-title2">БПЛА С-70 «Охотник»</p>
      <p class="aero-innovations-text-style-2">С-70 «Охотник» — российский тяжёлый ударный беспилотный летательный аппарат (БПЛА), разработанный компанией «Сухой». Предположительно, БПЛА имеет массу около 20 тонн, а при его разработке использовались технологии снижения радиолокационной заметности. БПЛА разрабатывается с использованием наработок и технологий истребителя пятого поколения Су-57. Радиолокационный комплекс и система связи позволяют использовать С-70 для расширения радиолокационного поля других боевых самолётов и дистанционного целеуказания; благодаря этому, например, появляется возможность применять средства поражения большой дальности без захода их носителя в зону действия ПВО противника. Истребитель Су-57 способен выполнять задачи в интеграции с БПЛА «Охотник». Предполагается, что БПЛА будет нести управляемые ракеты, управляемые бомбы, неуправляемые бомбы во внутреннем отсеке для полезной нагрузки, а также на подкрыльевых узлах подвески.</p>
      <p class="aero-innovations-text-style-2"><img src="/src/assets/user-svgrepo-com.svg" alt="" style="width: 25px; margin-bottom: 5px;"> Модель разработала: <b>Старикова Дарья</b></p>
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