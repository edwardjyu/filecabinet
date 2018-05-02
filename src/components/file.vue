<template>
  <div class="file">
    <!-- header -->
    <div class='header'>
      <div class="name">
        <div class="static" @click="status.fileNameEdit = true" v-if="!status.fileNameEdit">{{ file.name }}</div>
        <div class="edit" v-if="status.fileNameEdit">
          <input type="text" v-model="file.name" @keyup.enter="status.fileNameEdit = false">
        </div>
      </div>
      <div class="file-option">
        <div class="option-btn" @click="status.openFileOption=true">&#8231;&#8231;&#8231;</div>
        <div class="option-menu" v-if="status.openFileOption">
          <div class="option-header">
            <div class="title">Options</div>
            <div class="close" @click="status.openFileOption=false">&times;</div>
          </div>
          <div class="divider"></div>
          <div class="option-list">
            <div>Remove</div>
            <div>Sort</div>
          </div>
        </div>
      </div>
    </div>
    <!-- items -->
    <div class='items'>
      <div class="item" v-for="item in items" :key="item.key">
        <div class="name">{{ item.name }}</div>
        <div class="del" @click="delItem(file.key, item.key)">&times;</div>
      </div>
    </div>
    <!-- actions -->
    <div class='actions'>
      <div class='new-item-edit' v-if="status.newItemEdit">
        <input type='text' v-model="newItem">
        <div class='new-item-action'>
          <div class='btn' @click="addNewItem(file.key)">Add</div><div class='btn' @click.self="status.newItemEdit = false">&times;</div>
        </div>
      </div>
      <div class="new-item-action" v-else>
        <!--<div class='btn'>Browse...</div><div class='btn' @click="status.newItemEdit = true">Add a New</div>-->
        <div class='btn'>Browse...</div><div class='btn' @click="status.newItemEdit = true">Add a New</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'file',
  props: {
    file: null,
    items: []
  },
  data () {
    return {
      status: {
        fileNameEdit: false,
        newItemEdit: false,
        openFileOption: false
      },
      newItem: ''
    }
  },
  methods: {
    addNewItem: function (key) {
      if (this.newItem !== '') {
        const item = {
          key: Math.random().toString().slice(2, 10),
          name: this.newItem,
          parid: key
        }
        this.$emit('addItem', item)
        this.status.newItemEdit = false
        this.newItem = ''
      }
    },
    delItem: function (pkey, ckey) {
      this.$emit('remItem', pkey, ckey)
    },
    delFile: function (fkey) {
      this.$emit('delFile', fkey)
    }
  }
}
</script>

<style>
.file {
  width: 300px;
  margin: 10px;
  background-color: #e2e4e6;
  border-radius: 5px;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header .name {
  padding: 4px;
  width: 85%;
}

.header .name .static {
  height: 17px;
  font-weight: bolder;
  font-size: 14px;
  width: 100%;
  margin: 0;
  padding: 3px;
  cursor: pointer;
}

.header .name input {
  height: 17px;
  font-weight: bolder;
  font-size: 14px;
  width: 100%;
  margin: 0;
  padding: 3px;
  border: 1px solid #0079bf;
  box-shadow: 0 0 2px 0 #0284c6;
}

.header .option-btn {
  padding: 2px 4px;
  margin-right: 5px;
  color: #444;
  border-radius: 3px;
  text-align: center;
  cursor: pointer;
  position: relative;
}

.header .option-btn:hover {
  background-color: #cdd2d4;
}

.header .option-menu {
  display: flex;
  flex-direction: column;
  position: absolute;
  padding: 0;
  margin: 0;
  border-radius: 3px;
  background-color: white;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
}

.header .option-menu .option-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 10px;
  margin-left: 10px;
  margin-right: 10px;
}

.header .option-menu .title {
}

.header .option-menu .close {
  cursor: pointer;
}

.header .option-menu .divider {
  margin-left: 10px;
  margin-right: 10px;
  margin-bottom: 4px;
  border-bottom: 1px solid rgb(185, 185, 185);
}

.header .option-menu .option-list div {
  padding: 7px 20px;
}

.header .option-menu .option-list div:hover  {
  background-color: #5aac44;
  color: white;
}

.items {
  margin: 2px;
  padding: 4px;
}

.items .item {
  background-color: white;
  margin: 5px 0px;
  padding: 4px 6px;
  border-radius: 3px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 1px 1px rgba(0, 0, 0, 0.25);
}

.items .item .del {
  padding: 2px 4px;
  margin-right: 5px;
  border-radius: 3px;
  text-align: center;
  cursor: pointer;
}

.items .item .del:hover {
  background-color: #cdd2d4;
}

.actions {
  margin: 2px 2px 4px 2px;
  padding: 2px;
}

.actions .new-item-edit input[type="text"] {
  height: 30px;
  margin: 4px 2px;
  padding: 2px 4px;
  box-sizing: border-box;
  width: 288px;
  border-radius: 3px;
  border: none;
  box-shadow: 1px 1px rgba(0, 0, 0, 0.25);
}

.actions .new-item-action {
  display: flex;
  justify-content: flex-start;
}

.btn {
  padding: 4px 7px;
  margin: 1px 3px;
  color: white;
  background-color: #5aac44;
  text-align: center;
  border-radius: 3px;
}

.btn:hover {
  background-color: #519839;
}
</style>
