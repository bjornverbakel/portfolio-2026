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
  <main class="viewer">
    <section class="device-shell device-panel" aria-label="Portfolio device">
      <div class="console">
        <div class="screen-bezel">
          <div class="screen">
            <TresCanvas clear-color="#a9ebd4">
              <TresPerspectiveCamera
                :position="[0, 0, 30]"
                :look-at="[0, 0, 0]"
              />
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
                @pointerleave="
                  hoveredIcon === 'profile' && (hoveredIcon = null)
                "
              >
                <TresPlaneGeometry :args="[6.2, 7]" />
                <TresMeshBasicMaterial
                  transparent
                  :opacity="0"
                  :depth-write="false"
                />
              </TresMesh>

              <TresMesh
                :position="[0, 0.25, 2]"
                @pointerenter="hoveredIcon = 'folder'"
                @pointerleave="hoveredIcon === 'folder' && (hoveredIcon = null)"
              >
                <TresPlaneGeometry :args="[6.2, 7]" />
                <TresMeshBasicMaterial
                  transparent
                  :opacity="0"
                  :depth-write="false"
                />
              </TresMesh>

              <TresMesh
                :position="[10, 0.25, 2]"
                @pointerenter="hoveredIcon = 'envelope'"
                @pointerleave="
                  hoveredIcon === 'envelope' && (hoveredIcon = null)
                "
              >
                <TresPlaneGeometry :args="[6.2, 7]" />
                <TresMeshBasicMaterial
                  transparent
                  :opacity="0"
                  :depth-write="false"
                />
              </TresMesh>

              <EffectComposerPmndrs>
                <PixelationPmndrs :granularity="pixelSize" />
                <HueSaturationPmndrs :saturation="0.2" />
                <BrightnessContrastPmndrs :brightness="0.05" :contrast="0.13" />
              </EffectComposerPmndrs>
            </TresCanvas>
          </div>
        </div>
        <div class="speaker-panel">
          <div class="speaker-vent">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
          </div>
          <div class="speaker-label select-none">
            <div class="flex flex-col items-end leading-1">
              <span>MADE WITH</span>
              <span class="text-3xl">CSS</span>
            </div>

            <div class="label-lines">
              <span class="red"></span>
              <span class="yellow"></span>
              <span class="blue"></span>
            </div>
          </div>
          <div class="speaker-grille"></div>
          <div class="mic">
            <div class="flex flex-col justify-center items-center">
              <div class="led blue"></div>
              <p class="emboss-txt select-none">MIC</p>
            </div>
          </div>
        </div>

        <div class="button-panel sticker-txt">
          <div class="button-ridge" aria-hidden="true"></div>
          <div class="d-pad">
            <div class="d-pad-face">
              <button
                class="d-pad-direction d-pad-top"
                type="button"
                aria-label="Up"
              ></button>
              <button
                class="d-pad-direction d-pad-right"
                type="button"
                aria-label="Right"
              ></button>
              <button
                class="d-pad-direction d-pad-bottom"
                type="button"
                aria-label="Down"
              ></button>
              <button
                class="d-pad-direction d-pad-left"
                type="button"
                aria-label="Left"
              ></button>
              <button
                class="d-pad-center"
                type="button"
                aria-label="Confirm"
              ></button>
            </div>
          </div>
          <div class="console-buttons" aria-hidden="true">
            <button class="console-button" type="button">SELECT</button>
            <button class="console-button" type="button">START</button>
          </div>
        </div>
        <div class="decorative-panel">
          <div class="decorative-vent" aria-hidden="true">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
          </div>
          <div
            class="battery-indicator"
            role="img"
            aria-label="Battery indicator"
          >
            <div class="led green" aria-hidden="true"></div>
            <p class="emboss-txt select-none">BAT</p>
          </div>
          <button class="power-button" type="button" aria-label="Power">
            <span aria-hidden="true"></span>
          </button>
        </div>
      </div>
    </section>
  </main>
</template>
