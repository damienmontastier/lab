<script setup lang="ts">
import { PlaneGeometry, CircleGeometry, MathUtils } from 'three'
import { dispose } from '@tresjs/core';
import { Html } from '@tresjs/cientos';
import { useCssVar } from '@vueuse/core'



// Références aux éléments DOM pour appliquer les variables CSS dynamiques
const droitEl = ref(null);
const coucherEl = ref(null);

// Variables CSS dynamiques attachées aux éléments

watch(droitEl, () => {
  console.log(droitEl.value)

})

onMounted(() => {
  console.log(droitEl.value)
})

const droitColor = useCssVar('--color', droitEl, { initialValue: '#FFD700' });
const coucherColor = useCssVar('--color', coucherEl);

// Initialisation des couleurs
droitColor.value = '#FFD700'; // Couleur initiale pour "droit"
coucherColor.value = '#4682B4'; // Couleur initiale pour "coucher"

// Fonction pour mettre à jour les couleurs dynamiquement
const updateColors = (type, color) => {
  if (type === 'droit') {
    droitColor.value = color;
  } else if (type === 'coucher') {
    coucherColor.value = color;
  }
};

// Exemple : Fonction pour changer les couleurs dynamiquement
const changeColors = () => {
  updateColors('droit', '#FF5733'); // Nouvelle couleur pour "droit"
  updateColors('coucher', '#C70039'); // Nouvelle couleur pour "coucher"
};

const htmlRef = shallowRef(null)
const htmlReffffff = shallowRef(null)
const htmlRefff = shallowRef(null)
const testRef = shallowRef(null)
const testReffzsqsqqx = shallowRef(null)
const testRefffff = shallowRef(null)

testRef.value = new PlaneGeometry(40, 10);
testReffzsqsqqx.value = new CircleGeometry(7.5, 64);
testRefffff.value = new PlaneGeometry(.6, .2);

const { scene, nodes } = await useGLTF('/models/chair-configurator/sheen-chair.glb', { draco: true })

const onClickNode = (e) => {
  // e.stopPropagation()
  // console.log('click', e)
}

const onPointerMove = (e) => {
  // e.stopPropagation()
  // console.log('onPointerMove', e)
}

onUnmounted(() => {
  dispose(nodes.SheenChair_fabric)
  dispose(nodes.SheenChair_label)
  dispose(nodes.SheenChair_metal)
  dispose(nodes.SheenChair_wood)
})
</script>

<template>
  <TresGroup :scale="2">
    <primitive :object="nodes.SheenChair_fabric" @click="onClickNode" @pointer-move="onPointerMove" />
    <primitive :object="nodes.SheenChair_label" @click="onClickNode" @pointer-move="onPointerMove" />
    <primitive :object="nodes.SheenChair_metal" @click="onClickNode" @pointer-move="onPointerMove" />
    <primitive :object="nodes.SheenChair_wood" @click="onClickNode" @pointer-move="onPointerMove" />
  </TresGroup>

  <!-- DROIT -->
  <Html :zIndexRange="[-4, -6]" occlude="blending" ref="htmlRef" :geometry="testRef" center transform
    :position="[0, 1, -2.5]" wrapper-class="color-patch-wrapper droit" :distance-factor="8"
    @click="() => console.log('dehhdsqhdhdqsh click')">
  <div ref="droitEl" class="chair-configurator__color-patch droit"></div>

  </Html>

  <!-- COUCHER -->
  <Html :rotation-x="MathUtils.degToRad(90)" :zIndexRange="[-4, -6]" occlude="blending" ref="htmlReffffff"
    :geometry="testReffzsqsqqx" center transform :position="[0, -.5, 2]" wrapper-class="color-patch-wrapper coucher"
    :distance-factor="8" @click="() => console.log('dehhdsqhdhdqsh click')">
  <div ref="coucherEl " class="chair-configurator__color-patch coucher" />

  </Html>

  <Html @pointer-enter="(event) => console.log('pointer-enter')"
    @pointer-leave="(event) => console.log('pointer-leave')" :zIndexRange="[-2, -4]" occlude="blending" ref="htmlRefff"
    :geometry="testRefffff" center transform :position="[-.75, 1.4, -.45]"
    wrapper-class="chair-configurator__price-wrapper" @click="() => console.log('dehdddddddddddhdsqhdhdqsh click')"
    :distance-factor="2">

  <p class="chair-configurator__price">
    200€
  </p>

  </Html>
</template>

<style>
.chair-configurator__color-patch {
  border-radius: 50%;
  overflow: hidden;
}

.chair-configurator__color-patch.droit {
  width: 2000px;
  height: 500px;
  border-radius: 0%;
  background: linear-gradient(0deg, hsla(57, 100%, 48%, 1) 50%, hsla(204, 84%, 66%, 1) 75%);
}

.chair-configurator__color-patch.coucher {
  width: 750px;
  height: 750px;
  border-radius: 50%;
  background: linear-gradient(0deg, hsla(57, 100%, 48%, 1) 40%, hsla(204, 84%, 66%, 1) 60%);
}

.chair-configurator__price {
  border-radius: 20px;
  overflow: hidden;
  background: white;
  padding: 8px 20px;
  pointer-events: all !important;
}

.chair-configurator__price-wrapper {
  pointer-events: none;
}

.chair-configurator__price-wrapper:hover .chair-configurator__price {
  transform: scale(1.2);
}
</style>