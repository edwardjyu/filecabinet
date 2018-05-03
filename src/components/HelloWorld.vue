<template>
  <div>
    <h1>Categories</h1>
    <div class="file-cabinet">
      <file v-for="category in categories" :key="category.key" :file="category" :items="filteredItem(models, category.key)" @addItem="addModel" @remItem="removeModel" @delFile="delCat"></file>
    </div>
    <h1>Models</h1>
    <div class="file-cabinet">
      <file v-for="model in models" :key="model.key" :file="model" :items="filteredItem(products, model.key)" @addItem="addProduct" @remItem="removeProducts"></file>
    </div>
  </div>
</template>

<script>
import File from '@/components/File'

export default {
  name: 'HelloWorld',
  components: {
    'file': File
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      categories: [
        {key: 'abc', name: 'category #1'},
        {key: 'def', name: 'category #2'},
        {key: 'ghi', name: 'category #3'}
      ],
      models: [
        {key: '123', name: 'model #1', parid: 'abc'},
        {key: '456', name: 'model #2', parid: 'abc'},
        {key: '789', name: 'model #3', parid: 'abc'},
        {key: '101', name: 'model #4', parid: 'def'},
        {key: '111', name: 'model #5', parid: 'ghi'},
        {key: '213', name: 'model #6', parid: 'nmn'}
      ],
      products: [
        {key: 'jkl', name: 'product #1', parid: '123'},
        {key: 'mno', name: 'product #1', parid: '123'},
        {key: 'pqr', name: 'product #1', parid: '456'},
        {key: 'stu', name: 'product #1', parid: '456'},
        {key: 'vwx', name: 'product #1', parid: '111'},
        {key: 'yza', name: 'product #1', parid: '213'}
      ]
    }
  },
  methods: {
    filteredItem: function (items, key) {
      return items.filter((item) => {
        return item.parid === key
      })
    },
    removeModel: function (pkey, ckey) {
      this.models.forEach(element => {
        if (element.parid === pkey && element.key === ckey) {
          element.parid = null
        }
      })
    },
    addModel: function (model) {
      this.models.push(model)
    },
    delCat: function (fkey) {
      this.models.forEach(element => {
        if (element.parid === fkey) {
          element.parid = null
        }
      })
      this.categories = this.categories.filter((item) => {
        return item.key !== fkey
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.file-cabinet {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: flex-start;
  background: transparent;
}

</style>
