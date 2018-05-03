<template>
  <div class="wrapper">
    <div class="modal">
      <div class="header">
        <div class="title">Models</div>
        <div class="close-btn">&times;</div>
      </div>
      <div class="filter">
        <div id="selection"><input type="checkbox" id="checkbox" v-model="selectAll"><label for="checkbox">All</label></div>
        <div id="search"><input type="search" placeholder="Type the items to search" v-model="filter"></div>
      </div>
      <div class="item-container">
        <div class="item" v-for="(item, idx) in filteredItem" :key="item.key">
          <input type="checkbox" :id="'checkbox'+idx">
          <label :for="'checkbox'+idx">{{item.name}}</label>
        </div>
      </div>
      <div class="actions">
        <div class="btn" @click="register">Add</div><div class="btn">Cancel</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: []
  },
  data: function () {
    return {
      models: [
        {key: '123', name: 'model #1', parid: 'abc'},
        {key: '456', name: 'model #2', parid: 'abc'},
        {key: '789', name: 'model #3', parid: 'abc'},
        {key: '101', name: 'model #4', parid: null},
        {key: '111', name: 'model #5', parid: 'ghi'},
        {key: '213', name: 'model #6', parid: 'nmn'},
        {key: '141', name: 'model #7', parid: null},
        {key: '516', name: 'model #8', parid: null}
      ],
      selectAll: false,
      filter: null
    }
  },
  computed: {
    filteredItem: function () {
      let models = this.models
      if (this.selectAll === false) {
        models = models.filter(model => {
          return model.parid !== null
        })
      }

      if (this.filter) {
        models = models.filter(model => {
          return model.name.includes(this.filter)
        })
      }

      return models
    }
  },
  methods: {
    register: function () {
      this.$emit('registerItem', this.filteredItem)
    }
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.wrapper {
  font-size: 14px;
  font-family:Arial, Helvetica, sans-serif;
}

.modal {
  background: #f1f1f1;
  width: 70%;
  position: absolute;
  left: calc(50% - 35%);
  padding: 10px;
  box-shadow: 0 10px 30px rgba(51, 51, 51, 0.4);
  border: 1px solid #333333;
  /* visibility: hidden;
  opacity: 0; */
  top: 10%;
  visibility: visible;
  opacity: 1;
  transition: all 180ms ease-in;
  width: 580px;
}

.header {
  border-bottom: 1px solid #333333;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  text-transform: uppercase;
}

.header .title {
  font-size: 1rem;
  font-weight: 100;
  margin: 0;
}

.header .close-btn {
  font-size: 2rem;
  line-height: 2rem;
  cursor: pointer;
}

.filter {
  display: flex;
  justify-content: space-between;
  margin: 10px;
}

.filter #search
 {
  display: flex;
  justify-content: flex-end;
  align-items: center;
 }

 .filter input[type="text"] {
  margin-right: 10px;
 }

 .item-container {
  margin: 20px 10px;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
 }

.item-container .item {
  margin: 4px;
  color: white;
  user-select: none;
  text-align: center;
  width: 95px;
}

.item input[type="checkbox"] {
  display: none;
}

.item input[type="checkbox"] + label {
  padding: 8px 15px;
  background-color: #56a3eb;
  border-radius: 3px;
  display: inline-block;
}

.item input[type="checkbox"]:checked + label {
  background-color: #eb9e56;
}

.item-container .item .name {
   font-size: 1.2rem;
}

.item-container .item .description {
   font-size: 0.8rem;
 }

.actions {
  border-top: 1px solid #333333;
  margin-top: 10px;
  padding: 10px 0px;
  display: flex;
  justify-content: flex-end;
}
 .btn {
  padding: 4px 7px;
  margin: 1px 3px;
  color: white;
  background-color: #5aac44;
  text-align: center;
  border-radius: 3px;
}
</style>
