<script setup lang="ts">
import { inject, ref, type Ref } from "vue";
import { useIntervalFn } from "@vueuse/core";

import type { Colony } from "@/simulation";
import type { Simulation } from "./simulation";
import { RadioGroup, RadioOption } from "./forms";
import ColoniesChart from "./widgets/ColoniesChart.vue";

const simulation = inject<Simulation>("simulation")!;

const colonies = ref(simulation.garden.colonies) as Ref<Colony[]>;

useIntervalFn(() => {
  colonies.value = simulation.garden.colonies;
}, 200);

let tab = ref("domestic");
</script>

<template>
  <RadioGroup v-model="tab">
    <RadioOption label="内部" value="domestic" />
    <RadioOption label="战争" value="warfare" />
    <RadioOption label="总计" value="total" />
  </RadioGroup>

  <template v-if="tab === 'domestic'">
    <ColoniesChart
      :colonies="colonies"
      label="食物储备"
      field="food"
      :yAxisPrecision="0"
    />
    <ColoniesChart
      :colonies="colonies"
      label="存活蚂蚁数量"
      field="livingAnts"
    />
    <ColoniesChart :colonies="colonies" label="工蚁" field="workers" />
    <ColoniesChart :colonies="colonies" label="兵蚁" field="soldiers" />
  </template>

  <template v-if="tab === 'warfare'">
    <ColoniesChart
      :colonies="colonies"
      label="死亡数量"
      field="killedAnts"
      tooltip="Number of ants in this colony that were killed by other ants."
    />
    <ColoniesChart
      :colonies="colonies"
      label="Kills"
      field="killedEnemyAnts"
      tooltip="Number of enemy ants killed by this colony."
    />
    <ColoniesChart :colonies="colonies" label="Soldiers" field="soldiers" />
    <ColoniesChart
      :colonies="colonies"
      label="War coefficient"
      field="warCoef"
      :yAxisPrecision="3"
      tooltip="Increases when the ant that saw an enemy visits the nest. Higher values increase the chance of a soldier being born instead of a normal worker. Takes values between 0 and 1."
    />
  </template>

  <template v-if="tab === 'total'">
    <ColoniesChart :colonies="colonies" label="Total food" field="totalFood" />
    <ColoniesChart :colonies="colonies" label="Total ants" field="totalAnts" />
    <ColoniesChart
      :colonies="colonies"
      label="饥饿蚂蚁"
      field="starvedAnts"
    />
  </template>
</template>

<style scoped></style>
