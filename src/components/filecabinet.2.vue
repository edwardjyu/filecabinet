<template>
  <div class='file-cabinet'>
      <file v-for="f in files" :key="f.key" :file="f" :items="filteredItem(f.key)"></file>
  </div>
</template>

<script>
import File from '@/components/file'

export default {
  name: 'file-cabinet',
  components: { file: File },
  props: {
    files: [],
    items: []
  },
  data: function () {
    return {
    }
  },
  methods: {
    filteredItem: function (key) {
      return this.items.filter((item) => {
        return item.parid === key
      })
    }
  }
}
</script>

<style scoped>
.file-cabinet {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: flex-start;
  background: transparent;
}
</style>
