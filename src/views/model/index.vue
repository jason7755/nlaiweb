<template>
  <div>
    <waterfall :data="items" col="5" width="900px">
      <template>
        <div v-for="(item, index) in items" :key="index">
          <img :src="item.src" :alt="item.alt" width="200px">
        </div>
      </template>
    </waterfall>
  </div>
</template>

<script>
export default {
  // components: {
  //   waterfall
  // },
  data() {
    return {
      items: [
        { src: require('../../assets/images/jdb-ai-ad-1.png'), alt: 'img1' },
        { src: require('../../assets/images/jdb-ai-ad-9.png'), alt: 'img1' },
        { src: require('../../assets/images/jdb-ai-ad-23.png'), alt: 'img1' },
        { src: require('../../assets/images/jdb-ai-ad-61.png'), alt: 'img1' },
        { src: require('../../assets/images/jdb-ai-ad-9.png'), alt: 'img1' },
        { src: require('../../assets/images/jdb-ai-ad-23.png'), alt: 'img1' }
      ],
    };
  },
  created() {
    // this.items = await fetchImages()
    this.items.push({
      src: require('../../assets/images/jdb-ai-ad-1.png'),
      alt: 'img1'
    });
    this.items.push({
      src: require('../../assets/images/jdb-ai-ad-1.png'),
      alt: 'img1'
    });
    this.items.push({
      src: require('../../assets/images/jdb-ai-ad-1.png'),
      alt: 'img1'
    });
    this.items.push({
      src: require('../../assets/images/jdb-ai-ad-1.png'),
      alt: 'img1',
    });
    this.items.push({
      src: require('../../assets/images/jdb-ai-ad-1.png'),
      alt: 'img1'
    });
  },
};
</script>
