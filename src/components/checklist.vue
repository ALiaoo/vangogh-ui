<template>
  <div class="vg-checklist">
    <div class="checklist-wrapper" :class="{'show': isOpen}">
      <div class="top-bar">
        <span class="btn-cancel" @click="hide">取消</span>
        <span class="title">标题</span>
        <span class="btn-confirm" @click="onConfirm">完成</span>
      </div>
      <div class="desc-bar">
        <span class="desc">已选{{checkboxValue.length}}项</span>
        <span class="btn-clear" @click="clear">清空</span>
      </div>
      <div class="list">
        <div class="item-wrapper" v-for="(item, index) in data" :data-val="item.id + '|' + item.title + '|' + item.desc">
          <input type="checkbox" :id="index" v-model="checkboxValue" @click="selectedItem($event)" style="display:none" :value="item.id + '|' + item.title + '|' + item.desc">
          <label :for="index" class="item">
            <div class="left"></div>
            <div class="right">
              <div class="title">{{ item.title }}</div>
              <div class="author">{{ item.desc }}</div>
            </div>
          </label>
        </div>
      </div>
    </div>
    <div class="mask" v-if="isOpen"></div>
  </div>
</template>

<script>
export default {
  name: 'Checklist',
  props: {
    max: {
      type: Number,
      default: 0
    },
    data: {
      type: Array
    }
  },
  data () {
    return {
      checkboxValue: [],
      isOpen: false
    }
  },
  methods: {
    selectedItem (event) {
      // 获取当前节点之后的下一个兄弟元素
      const labelNode = event.target.nextElementSibling
      const classList = labelNode.classList
      // 绑定selected
      classList.contains('selected') ? classList.remove('selected') : classList.add('selected')
    },
    show () {
      this.isOpen = true
    },
    hide () {
      this.isOpen = false
    },
    clear () {
      this.checkboxValue = []
    },
    onConfirm () {
      this.isOpen = false
      const checkboxValue = this.checkboxValue
      const results = []
      checkboxValue.map(v => {
        const item = v.split('|')
        results.push({
          id: item[0],
          title: item[1],
          desc: item[2]
        })
      })
      // 触发事件
      this.$emit('on-change', results)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .vg-checklist {
    overflow: hidden;
  }

  .checklist-wrapper {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    background-color: #fff;
    -webkit-transition: all .5s;
    transition: all .5s;
    -webkit-transform: translateY(100%);
    transform: translateY(100%);
    z-index: 10;
  }

  .checklist-wrapper.show {
    -webkit-transform: translateY(0%);
    transform: translateY(0%);
  }

  .top-bar {
    height: 30px;
    padding: 5px 10px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid #ddd;
  }

  .btn-cancel {
    color: #9F9F9F;
  }

  .btn-confirm {
    color: #1799fa;
  }

  .desc-bar {
    height: 30px;
    padding: 10px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid #ddd;
  }

  .list {
    max-height: 300px;
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

  .left {
    width: 20px;
    height: 20px;
    background-color: #fff;
    position: relative;
    border:1px solid #9e9e9e;
  }

  .item.selected .left {
    border: 1px solid #1799fa;
    background-color: #1799fa;
  }

  .item.selected .left::before {
    content: ' ';
    position: absolute;
    width: 14px;
    height: 14px;
    top: 3px;
    left: 3px;
    background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABUAAAAPCAYAAAALWoRrAAAA90lEQVQ4ja3TMSuFURgH8GeQRGIwy6BkUbIYlHwBu0Umi8VkMVlMJoMvIcNdDAYlJuULWCSESBSLwc9we/P2eu715t6nznKe//Or0zknEF1YS3jAHRa7Aa7iy0/ddAquVUC47ARcT8APLPwX3PC73jGPCPRiGSvoqwFuJuAb5opMoFFqnmCwDbiVgK+YLecCn5XQGYYScDsBXzBTzQb2k/A5hkvBnSTzhOnsRIEBHCdDFxjBbtJ7xFQGFmigH0fJ8HOyd4/JVmAZDc2bP0yQct1ioh1YRYvn1cg0XGP8LzBDC/igAl5hrA7YCg30YE/zl5xitC6I+AYJmBaJbbKurAAAAABJRU5ErkJggg==");
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center center;
    z-index: 1;
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

  .mask {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, .5);
    transition: all .5s;
  }

</style>
