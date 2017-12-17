<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="demo" @click="openChecklist">
      <span>custom checklist demo</span>
    </div>
    <div class="list">
      <div class="item" v-for="(item, index) in results" :data-val="index">
        <div class="left">{{ index + 1 }}</div>
        <div class="right">
          <div class="title">{{ item.title }}</div>
          <div class="author">{{ item.desc }}</div>
        </div>
      </div>
    </div>
    <vg-checklist ref="checklist" :data="data" :max="5" @on-change="onChange"></vg-checklist>
  </div>
</template>

<script>
  import Checklist from './checklist'
  export default {
    name: 'Demo',
    components: {
      'vg-checklist': Checklist
    },
    data () {
      return {
        msg: 'Demo list',
        data: [
          {
            id: '1',
            title: 'Starry Starry Night',
            desc: 'Clint Mansell —— Loving Vincent'
          },
          {
            id: '2',
            title: 'The Night Cafe',
            desc: 'Clint Mansell  —— Loving Vincent'
          },
          {
            id: '3',
            title: 'The Yellow House',
            desc: 'Clint Mansell s —— Loving Vincent'
          },
          {
            id: '4',
            title: 'Portrait Of Armand Roulin',
            desc: 'Clint Mansell  —— Loving Vincent'
          },
          {
            id: '5',
            title: 'Five Sunflowers in A Vase',
            desc: 'Clint Mansell  —— Loving Vincent'
          },
          {
            id: '6',
            title: 'Wheatfield With Crows',
            desc: 'Clint Mansell  —— Loving Vincent'
          }
        ],
        results: []
      }
    },
    methods: {
      openChecklist () {
        this.$refs['checklist'].show()
      },
      onChange (val) {
        console.log('val', val)
        this.results = val
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .demo {
    padding: 10px 15px;
    border-top: 1px solid #ddd;
    border-bottom: 1px solid #ddd;
  }

  .list {
    margin-top: 20px;
    max-height: 500px;
    overflow-y: auto;
    -webkit-overflow-scrolling: touch;
    overflow-scrolling: touch;
  }

  .item {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px 15px;
  }

  .right {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    border-bottom: 1px solid #ddd;
    margin-left: 15px;
  }

</style>
