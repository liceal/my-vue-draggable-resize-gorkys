<template>
  <div id="app">
    <h1>个人</h1>
    <My/>

    <h1>官方</h1>

    <div style="height: 800px; width: 1200px; border: 1px solid red; position: relative;margin: 0 auto">
      <vue-draggable-resizable
        :w="200"
        :h="200"
        :parent="true"
        :debug="false"
        :min-width="200"
        :min-height="200"
        :isConflictCheck="true"
        :snap="true"
        :snapTolerance="1"
        @refLineParams="getRefLineParams"
        class="test1">
      </vue-draggable-resizable>
      <vue-draggable-resizable
        :w="200"
        :h="200"
        :parent="true"
        :x="210"
        :debug="false"
        :min-width="200"
        :min-height="200"
        :isConflictCheck="true"
        :snap="true"
        :snapTolerance="1"
        @refLineParams="getRefLineParams"
        class="test2">
      </vue-draggable-resizable>
      <vue-draggable-resizable
        :w="200"
        :h="200"
        :parent="true"
        :x="420"
        :debug="false"
        :min-width="200"
        :min-height="200"
        :isConflictCheck="true"
        :snap="true"
        :snapTolerance="1"
        @refLineParams="getRefLineParams"
        class="test3">
      </vue-draggable-resizable>
      <!--辅助线-->
      <span class="ref-line v-line"
            v-for="item in vLine"
            :key="item.id"
            v-show="item.display"
            :style="{ left: item.position, top: item.origin, height: item.lineLength}"
      />
      <span class="ref-line h-line"
            v-for="item in hLine"
            :key="item.id"
            v-show="item.display"
            :style="{ top: item.position, left: item.origin, width: item.lineLength}"
      />
      <!--辅助线END-->
    </div>
  </div>
</template>

<script>
import VueDraggableResizable from './components/vue-draggable-resizable'
import './components/vue-draggable-resizable.css'
import My from './my.vue'
export default {
  name: 'app',
  components: {
    VueDraggableResizable,
    My
  },
  data () {
    return {
      vLine: [],
      hLine: []
    }
  },
  methods: {
    // 辅助线回调事件
    getRefLineParams (params) {
      const { vLine, hLine } = params
      let id = 0
      this.vLine = vLine.map(item => {
        item['id'] = ++id
        return item
      })
      this.hLine = hLine.map(item => {
        item['id'] = ++id
        return item
      })
    }
  }
}
</script>

<style>
  .test1 {
    background-color: rgb(239, 154, 154);
  }
  .test2{
    background-color: rgb(129, 212, 250);
  }
  .test3{
    background-color: rgb(174, 213, 129);
  }
</style>
