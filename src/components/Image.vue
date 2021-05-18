<template>
  <img :alt="alt" :src="require(`@/assets/${image}`)" />
</template>

<script>
export default {
  name: 'Image',
  props: {
    alt: String,
    image: String
  }
}
</script>
