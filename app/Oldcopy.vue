<template>
  <div>

    <ClientOnly>
      <Button label="Verify" class=" " />


      <Galleria :value="images" :responsiveOptions="responsiveOptions" :numVisible="5" :circular="true"
        containerStyle="max-width: 640px" :showItemNavigators="true" :showThumbnails="false">
        <template #item="slotProps">
          <img :src="slotProps.item.itemImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block;" />
        </template>
        <template #thumbnail="slotProps">
          <img :src="slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" style="display: block;" />
        </template>
      </Galleria>


      <div class="card flex justify-center">
        <Galleria v-model:activeIndex="activeIndex" v-model:visible="displayCustom" :value="images"
          :responsiveOptions="responsiveOptions" :numVisible="7" containerStyle="max-width: 850px" :circular="true"
          :fullScreen="true" :showItemNavigators="true" :showThumbnails="false">
          <template #item="slotProps">
            <img :src="slotProps.item.itemImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block" />
          </template>
          <template #thumbnail="slotProps">
            <img :src="slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" style="display: block" />
          </template>
        </Galleria>

        <div v-if="images" class="grid grid-cols-12 gap-4" style="max-width: 400px">
          <div v-for="(image, index) of images" :key="index" class="col-span-4">
            <img :src="image.thumbnailImageSrc" :alt="image.alt" style="cursor: pointer" @click="imageClick(index)" />
          </div>
        </div>
      </div>


    </ClientOnly>

  </div>

</template>

<script setup>




const images = ref([
  {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria1.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria1s.jpg',
    alt: 'Description for Image 1',
    title: 'Title 1'
  }, {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria2.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria2s.jpg',
    alt: 'Description for Image 2',
    title: 'Title 2'
  }, {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria3.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria3s.jpg',
    alt: 'Description for Image 3',
    title: 'Title 3'
  }, {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria4.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria4s.jpg',
    alt: 'Description for Image 4',
    title: 'Title 4'
  }, {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria5.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria5s.jpg',
    alt: 'Description for Image 5',
    title: 'Title 5'
  },
]);
const activeIndex = ref(0);
const responsiveOptions = ref([
  {
    breakpoint: '991px',
    numVisible: 4
  },
  {
    breakpoint: '767px',
    numVisible: 3
  },
  {
    breakpoint: '575px',
    numVisible: 1
  }
])
const displayCustom = ref(false);
const imageClick = (index) => {
    activeIndex.value = index;
    displayCustom.value = true;
};
</script>
