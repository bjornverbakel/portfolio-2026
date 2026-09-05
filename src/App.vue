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
import IconMotion from "./components/IconMotion.vue";
import DeviceShell from "./components/device/DeviceShell.vue";
import {
  AmbientLight,
  DirectionalLight,
  Group,
  Mesh,
  MeshBasicMaterial,
  PerspectiveCamera,
  PlaneGeometry,
} from "three";

extend({
  AmbientLight,
  DirectionalLight,
  Group,
  Mesh,
  MeshBasicMaterial,
  PerspectiveCamera,
  PlaneGeometry,
});

const pixelSize = ref(4);
const profile = ref(null);
const folder = ref(null);
const envelope = ref(null);
const hoveredIcon = ref(null);
</script>

<template>
  <DeviceShell>
    <TresCanvas clear-color="#a9ebd4">
      <TresPerspectiveCamera :position="[0, 0, 30]" :look-at="[0, 0, 0]" />
      <TresAmbientLight :intensity="1.25" />
      <TresDirectionalLight :position="[3, 5, 4]" :intensity="1.75" />

      <IconMotion
        :hovered="hoveredIcon === 'profile'"
        :position="[-10, 0, 0]"
        :float-delay="0"
      >
        <GLTFModel
          ref="profile"
          path="/models/profile.glb"
          :scale="1.3"
          :position="[0, 0, 0]"
          :rotation="[0, Math.PI / 2, 0]"
        />
      </IconMotion>

      <IconMotion
        :hovered="hoveredIcon === 'folder'"
        :position="[0, -1.5, 0]"
        :float-delay="2"
      >
        <GLTFModel
          ref="folder"
          path="/models/folder.glb"
          :scale="1"
          :position="[0, 0, 0]"
          :rotation="[0, Math.PI / 2, 0]"
        />
      </IconMotion>

      <IconMotion
        :hovered="hoveredIcon === 'envelope'"
        :position="[10, -1, 0]"
        :float-delay="4"
      >
        <GLTFModel
          ref="envelope"
          path="/models/envelope.glb"
          :scale="1"
          :position="[0, 0, 0]"
          :rotation="[0, Math.PI / 2, 0]"
        />
      </IconMotion>

      <TresMesh
        :position="[-10, 0.25, 2]"
        @pointerenter="hoveredIcon = 'profile'"
        @pointerleave="hoveredIcon === 'profile' && (hoveredIcon = null)"
      >
        <TresPlaneGeometry :args="[6.2, 7]" />
        <TresMeshBasicMaterial transparent :opacity="0" :depth-write="false" />
      </TresMesh>

      <TresMesh
        :position="[0, 0.25, 2]"
        @pointerenter="hoveredIcon = 'folder'"
        @pointerleave="hoveredIcon === 'folder' && (hoveredIcon = null)"
      >
        <TresPlaneGeometry :args="[6.2, 7]" />
        <TresMeshBasicMaterial transparent :opacity="0" :depth-write="false" />
      </TresMesh>

      <TresMesh
        :position="[10, 0.25, 2]"
        @pointerenter="hoveredIcon = 'envelope'"
        @pointerleave="hoveredIcon === 'envelope' && (hoveredIcon = null)"
      >
        <TresPlaneGeometry :args="[6.2, 7]" />
        <TresMeshBasicMaterial transparent :opacity="0" :depth-write="false" />
      </TresMesh>

      <EffectComposerPmndrs>
        <PixelationPmndrs :granularity="pixelSize" />
        <HueSaturationPmndrs :saturation="0.2" />
        <BrightnessContrastPmndrs :brightness="0.05" :contrast="0.13" />
      </EffectComposerPmndrs>
    </TresCanvas>
  </DeviceShell>
</template>
