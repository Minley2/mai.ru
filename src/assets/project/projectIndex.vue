<script setup lang="ts">
import { ref } from "vue";

import su25 from "./su25.vue";
import mig35 from "./mig35.vue";
import mirage from "./mirage.vue";
import geran from "./geran.vue";
import boeing777 from "./boeing777.vue";
import an225 from "./an225.vue";
import su30 from "./su30.vue";
import yak38 from "./yak38.vue";
import lancet from "./lancet.vue";
import tahion from "./tahion.vue";
import reys from "./reys.vue";
import j10 from "./j10.vue";
import an2 from "./an2.vue";
import tu144 from "./tu144.vue";
import yak141 from "./yak141.vue";
import mig15 from "./mig15.vue";
import su15 from "./su15.vue";
import beluga from "./beluga.vue";
import ohotnik from "./ohotnik.vue";
import il76 from "./il76.vue";
import su24 from "./su24.vue";

const menu = ref();
menu.value = [
    {id: 1, name: "Су-25"},
    {id: 2, name: "МиГ-35"},
    {id: 3, name: "Mirage 2000"},
    {id: 4, name: "БПЛА «Герань»"},
    {id: 5, name: "Boeing 777"},
    {id: 6, name: "Ан-225"},
    {id: 7, name: "Су-30"},
    {id: 8, name: "Як-38"},
    {id: 9, name: "БПЛА «Ланцет»"},
    {id: 10, name: "БПЛА «Тахион»"},
    {id: 11, name: "БПЛА Ту-143 «Рейс»"},
    {id: 12, name: "Chengdu J-10"},
    {id: 13, name: "Ан-2"},
    {id: 14, name: "Ту-144"},
    {id: 15, name: "Як-141"},
    {id: 16, name: "МиГ-15"},
    {id: 17, name: "Су-15"},
    {id: 18, name: "Airbus Beluga"},
    {id: 19, name: "БПЛА С-70 «Охотник»"},
    {id: 20, name: "Ил-76"},
    {id: 21, name: "Су-24"},
];

function getRandomNumber(min: number, max: number): number {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
const currentMenuId = ref(getRandomNumber(1, menu.value.length));
// const currentMenuId = ref(21);

function getMenuId(id: number) {
  currentMenuId.value = id;
}
</script>

<template>
    <div class="example">
    <div class="dropdown" style="text-align: center;">
    <button class="btn btn-primary btn-lg dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false">
        Выберите модель
    </button>
    <ul class="dropdown-menu dropdown-menu-dark">
    <li :class="currentMenuId === item.id ? 'active' : ''"
          v-for="(item, index) in menu"
          :key="item.id"
          @click="getMenuId(item.id)"><a :class="currentMenuId === item.id ? 'active' : ''" class="dropdown-item" href="javascript:void(0)">{{ item.name }}</a></li>
    </ul>
    </div>
    <su25 v-if="currentMenuId === 1"/>
    <mig35 v-if="currentMenuId === 2"/>
    <mirage v-if="currentMenuId === 3"/>
    <geran v-if="currentMenuId === 4"/>
    <boeing777 v-if="currentMenuId === 5"/>
    <an225 v-if="currentMenuId === 6"/>
    <su30 v-if="currentMenuId === 7"/>
    <yak38 v-if="currentMenuId === 8"/>
    <lancet v-if="currentMenuId === 9"/>
    <tahion v-if="currentMenuId === 10"/>
    <reys v-if="currentMenuId === 11"/>
    <j10 v-if="currentMenuId === 12"/>
    <an2 v-if="currentMenuId === 13"/>
    <tu144 v-if="currentMenuId === 14"/>
    <yak141 v-if="currentMenuId === 15"/>
    <mig15 v-if="currentMenuId === 16"/>
    <su15 v-if="currentMenuId === 17"/>
    <beluga v-if="currentMenuId === 18"/>
    <ohotnik v-if="currentMenuId === 19"/>
    <il76 v-if="currentMenuId === 20"/>
    <su24 v-if="currentMenuId === 21"/>
    </div>
</template>

<style>
.example {
  height: 100%;
}
</style>