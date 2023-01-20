<script setup lang="ts">
import { inject } from "vue";
import predefinedMaps from "./maps/predefinedMaps";
import { loadMap } from "./maps/utils";
import type { Simulation } from "./simulation";
import { state } from "./state";
import Modal from "./widgets/Modal.vue";

let simulation = inject<Simulation>("simulation")!;

function startTour() {
  state.tourMode = true;
  hideWelcome();
  loadMap(simulation, "1: Single ant", predefinedMaps.tour);
}

function skipTour() {
  state.tourMode = false;
  hideWelcome();
}

function hideWelcome() {
  state.isWelcomed = true;
  localStorage.setItem("isWelcomed", "true");
}
</script>

<template>
  <Modal :show-header="false" :showActions="false">
    <template v-slot:content>
      <h1>欢迎使用&nbsp;蚁群仿真平台</h1>

      <p>
        这是一个算法仿真的构架设计和多种策略的技术实现。
      </p>

      <div class="actions">
        <button class="btn btn-primary" @click="startTour">功能漫游</button>

        <button class="btn btn-secondary" @click="skipTour">跳过向导</button>
      </div>
    </template>
  </Modal>
</template>

<style scoped>
h1 {
  text-align: center;
  border-bottom: 5px solid #486042;
}
p {
  margin: 20px 0;
  text-align: center;
}
.actions {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}
.btn-primary {
  padding: 20px;
  font-size: 20px;
}
</style>
