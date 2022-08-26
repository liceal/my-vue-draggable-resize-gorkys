<template>
  <div id="app">

    <!-- list -->
    <p>
      {{list}}
    </p>
    <div
      style="height: 500px; width: 500px; border: 1px solid red; position: relative;"
    >
      <draggable v-model="list" item-key="id" style="height:100%" group="group1">
        <div class="draggable-resizable" v-for="l in list" :key="l.id">
          <vue-draggable-resizable
            :grid=[20,20]
            :draggable="false"
            :w="200"
            :h="200"
            :parent="false"
            :min-width="50"
            :min-height="50"
            :ref="resizeNodeRef(l.id)"
            @resizing="(x,y,w,h)=>resizeHandle({x,y,w,h,l})"
          >
            <p>vue-draggable-resizable{{l.id}}</p>
          </vue-draggable-resizable>
        </div>

        <!-- <vue-draggable-resizable
          class="draggable-resizable"
          v-for="l in list"
          :key="l.id"
          :grid=[20,20]
          :draggable="false"
          :w="200"
          :h="200"
          :parent="false"
          :min-width="50"
          :min-height="50"
          :ref="resizeNodeRef(l.id)"
          @resizing="(x,y,w,h)=>resizeHandle({x,y,w,h,l})"
        >
          <p>vue-draggable-resizable{{l.id}}</p>
        </vue-draggable-resizable> -->

      </draggable>

    </div>

    <!-- list1 -->
    <p>
      {{list1}}
    </p>
    <div
      style="height: 500px; width: 500px; border: 1px solid red; position: relative;"
      id="list1-container"
    >
      <draggable v-model="list1" item-key="id" style="height:100%" group="group1" handle=".drag-handle">
        <div v-for="l in list1" :key="l.id">
          <vue-draggable-resizable
            :grid=[20,20]
            :draggable="true"
            :w="200"
            :h="200"
            parent="#list1-container"
            :min-width="50"
            :min-height="50"
            :ref="resizeNodeRef(l.id)"
            drag-handle=".resize-handle"
          >
            <b class="resize-handle handle1">按我拖动块</b>
            <b class="drag-handle handle1">按我切换位置</b>
            <p>vue-draggable-resizable{{l.id}}</p>
          </vue-draggable-resizable>
        </div>

        <!-- <vue-draggable-resizable
          v-for="l in list1"
          :key="l.id"
          :grid=[20,20]
          :draggable="true"
          :w="200"
          :h="200"
          :parent="true"
          :min-width="50"
          :min-height="50"
          :ref="resizeNodeRef(l.id)"
          drag-handle=".resize-handle"
        >
          <b class="resize-handle handle1">按我拖动块</b>
          <b class="drag-handle handle1">按我切换位置</b>
          <p>vue-draggable-resizable{{l.id}}</p>
        </vue-draggable-resizable> -->

      </draggable>

    </div>

    <!-- list2 -->
    <p>
      {{list2}}
    </p>
    <div
      style="height: 500px; width: 500px; border: 1px solid red; position: relative;"
    >
      <draggable v-model="list2" item-key="id" style="height:100%" group="group1">
          <!-- <vue-draggable-resizable
          :draggable="false"
            v-for="l in list" :key="l.id"
            :w="200"
            :h="200"
            :parent="false"
            :min-width="50"
            :min-height="50"
          >
            <p>vue-draggable-resizable</p>
          </vue-draggable-resizable> -->
          <p v-for="l in list2" :key="l.id">
            {{l.id}}
          </p>
      </draggable>

    </div>

    <div
      style="height: 500px; width: 500px; border: 1px solid red; position: relative;"
    >
      <vue-draggable-resizable
        :w="200"
        :h="200"
        :parent="true"
        :min-width="50"
        :min-height="50"
      >
        <p>vue-draggable-resizable</p>
      </vue-draggable-resizable>

      <vue-draggable-resizable
        :x="150"
        :y="150"
        :w="200"
        :h="200"
        :parent="true"
        :min-width="50"
        :min-height="50"
      >
        <p>vue-draggable-resizable</p>
      </vue-draggable-resizable>
    </div>
  </div>
</template>

<script>
import VueDraggableResizable from './components/vue-draggable-resizable'
import './components/vue-draggable-resizable.css'
import draggable from 'vuedraggable'

export default {
  name: 'app',
  components: {
    VueDraggableResizable,
    draggable
  },
  data () {
    return {
      list: [
        { id: 1 },
        { id: 2 },
        { id: 3 }
      ],
      list1: [
        { id: 4 }
      ],
      list2: []
    }
  },
  methods: {
    resizeHandle: function ({ x, y, w, h, l }) {
      // this.$refs[this.resizeNodeRef(l.id)]
      const el = this.$refs[this.resizeNodeRef(l.id)][0].$el
      el.style.marginTop = `${y}px`
      el.style.marginLeft = `${x}px`
    },
    resizeNodeRef (id) {
      return `resize${id}`
    }
  }
}
</script>

<style>
.vdr {
  border: 1px dashed black;
}
p{
  background:pink;
}
.draggable-resizable{
  position: relative;
  /* display: inline-block; */
  float:left;
}
.draggable-resizable .vdr{
  position: relative;
  background:LightPink;
  transform: none !important;
}
.handle1{
  cursor: pointer;
  background: #ccc;
}
.handle1 + .handle1{
  margin-left:5px;
}
</style>
