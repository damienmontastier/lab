<script setup lang="ts">
import { TresCanvas } from '@tresjs/core'
import { BasicShadowMap, SRGBColorSpace, AgXToneMapping, CircleGeometry, MathUtils } from 'three'
import { OrbitControls, Html } from '@tresjs/cientos';
/* import { EffectComposer, Bloom } from '@tresjs/post-processing' */
import { BlendFunction } from 'postprocessing'

const gl = {
  clearColor: '#ffffff',
  shadows: true,
  alpha: true,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: AgXToneMapping,
}
</script>

<template>
  <TresCanvas v-bind="gl" window-size class="canvas-chair-configurator">
    <TresPerspectiveCamera :position="[-2.5, 2.15, 3]" :near="0.001" />
    <OrbitControls make-default :target="[0, .65, 0]" :enable-pan="false" />

    <Suspense>
      <Chair />
    </Suspense>

    <ContactShadows :position-y="0" color="#000000" :blur=".35" :opacity=".25" :scale="5" />

    <Suspense>
      <Environment preset="city" />
    </Suspense>

    <TresAmbientLight :args="[0x404040, 0.7]" />

  </TresCanvas>
</template>

<style>
.canvas-chair-configurator {
  height: 100%;
  width: 100%;
  cursor: grab;
  position: fixed;
  top: 0;
  left: 0;
}
</style>