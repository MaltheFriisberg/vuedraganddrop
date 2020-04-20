<template>
  <div>
    <div 
    @drop='onDrop($event, 1)' 
      @dragover.prevent
      @dragenter.prevent
    class='drop-zone'>
      <div v-for='item in listOne' :key='item.title' draggable
        @dragstart='startDrag($event, item)' 
        class='drag-el'>
        {{ item.title }}
      </div>
    </div>
    <div 
    @drop='onDrop($event, 2)' 
      @dragover.prevent
      @dragenter.prevent
    class='drop-zone'>
      <div v-for='item in listTwo' :key='item.title' draggable
        @dragstart='startDrag($event, item)' 
         class='drag-el'>
        {{ item.title }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
   data () {
    return {
      items: [
      {
        id: 0,
        title: 'Item A',
        list: 1
      },
      {
        id: 1,
        title: 'Item B',
        list: 1
      },
      {
        id: 2,
        title: 'Item C',
        list: 2
      },
      {
        id: 3,
        title: 'Item D',
        list: 2
      }]
    }
  },
  computed: {
    listOne () {
      return this.items.filter(item => item.list === 1)
    },
    listTwo () {
      return this.items.filter(item => item.list === 2)
    }
  },
  methods:{
    startDrag: (evt, item) => {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemID', item.id)
    },
    onDrop (evt, list) {
      console.log('onDrop' +evt);
      console.log('onDrop' +list);
      const itemID = evt.dataTransfer.getData('itemID')
      const item = this.items.find(item => item.id == itemID)
      item.list = list
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.drop-zone {
    background-color: blue;
    margin-bottom: 10px;
    padding: 10px;
    height: 500px;
  }

  .drag-el {
    background-color: #fff;
    margin-bottom: 10px;
    padding: 5px;
  }
</style>
