<template>
  <div class='file-cabinet'>
    <!-- file -->
    <div class="file" v-for="file in files" :key="file.key">
      <!-- header -->
      <div class='header'>
        <div class="name">
          <div class="static" @click="status.fileNameEdit = true" v-if="!status.fileNameEdit">{{ file.name }}</div>
          <div class="edit" v-if="status.fileNameEdit">
            <input type="text" v-model="file.name" @keyup.enter="status.fileNameEdit = false">
          </div>
        </div>
        <div class="option">&#8231;&#8231;&#8231;</div>
      </div>
      <!-- items -->
      <div class='items'>
        <div class="item" v-for="item in items" :key="item.key">
          <div class="name">{{ item.name }}</div>
          <div class="del">&times;</div>
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
          <div class='btn'>Browse...</div><div class='btn' @click="openNewItemEdit($event)">Add a New</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'file-cabinet',
  props: {
    files: [],
    items: []
  },
  data: function () {
    return {
      status: {
        fileNameEdit: true,
        newItemEdit: false
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
        this.items.push(item)
        this.status.newItemEdit = false
        this.newItem = ''
      }
    },
    openNewItemEdit: function (e) {
      console.log(e)
    }
  }
}
</script>

<style scoped>
.file-cabinet {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  background: transparent;
}

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

.header .option {
  padding: 2px 4px;
  margin-right: 5px;
  color: #444;
  border-radius: 3px;
  text-align: center;
  cursor: pointer;
}

.header .option:hover {
  background-color: #cdd2d4;
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
