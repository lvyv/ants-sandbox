<script setup lang="ts">
import { Tabs, Tab } from "./widgets";
import Simulation from "./Simulation.vue";
import Draw from "./Draw.vue";
import Maps from "./maps/Maps.vue";
import Visuals from "./visuals/Visuals.vue";
import Colonies from "./colonies/Colonies.vue";
import NewGarden from "./NewGarden.vue";
import Charts from "./Charts.vue";
import About from "./About.vue";
</script>

<template>
  <div class="menu">
    <Tabs>
      <Tab label="新建">
        <NewGarden />
      </Tab>
      <Tab label="地图">
        <Maps />
      </Tab>
      <Tab label="绘制">
        <Draw />
      </Tab>
      <Tab label="蚁群">
        <Colonies />
      </Tab>
      <Tab label="图表">
        <Charts />
      </Tab>
      <Tab label="仿真">
        <Simulation />
      </Tab>
      <Tab label="可视化">
        <Visuals />
      </Tab>
      <Tab label="关于">
        <About />
      </Tab>
    </Tabs>
  </div>
</template>

<style>
.menu {
  max-width: 100vw;
}
</style>
