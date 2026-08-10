<script setup>
import { ref } from "vue";
import { TresCanvas, extend } from "@tresjs/core";
import {
  BrightnessContrastPmndrs,
  EffectComposerPmndrs,
  HueSaturationPmndrs,
  PixelationPmndrs,
} from "@tresjs/post-processing";
import { GLTFModel } from "@tresjs/cientos";
import {
  AmbientLight,
  CapsuleGeometry,
  DirectionalLight,
  Group,
  Mesh,
  MeshStandardMaterial,
  PerspectiveCamera,
  PlaneGeometry,
  SphereGeometry,
} from "three";

extend({
  AmbientLight,
  CapsuleGeometry,
  DirectionalLight,
  Group,
  Mesh,
  MeshStandardMaterial,
  PerspectiveCamera,
  PlaneGeometry,
  SphereGeometry,
});

const pixelSize = ref(7);
const profile = ref(null);
</script>

<template>
  <main class="viewer">
    <TresCanvas clear-color="#d8f0e5">
      <TresPerspectiveCamera :position="[0, 0, 10]" :look-at="[0, 0, 0]" />
      <TresAmbientLight :intensity="1.25" />
      <TresDirectionalLight :position="[3, 5, 4]" :intensity="1.75" />

      <GLTFModel
        ref="profile"
        path="/models/profile.glb"
        :scale="1"
        :position="[0, -3.35, 0]"
        :rotation="[0, Math.PI / 2, 0]"
      />

      <TresMesh :rotation="[-Math.PI / 2, 0, 0]" :position="[0, -3.35, 0]">
        <TresPlaneGeometry :args="[20, 20]" />
        <TresMeshStandardMaterial color="#8fcab5" roughness="1" />
      </TresMesh>

      <EffectComposerPmndrs>
        <PixelationPmndrs :granularity="pixelSize" />
        <HueSaturationPmndrs :saturation="0.2" />
        <BrightnessContrastPmndrs :brightness="0.05" :contrast="0.13" />
      </EffectComposerPmndrs>
    </TresCanvas>
  </main>
</template>
