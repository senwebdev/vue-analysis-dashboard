<template>
  <section
    class="dashboard"
    v-packery="{
      itemSelector: '.dashboard-item',
      columnWidth: '.grid-sizer',
      gutter: '.gutter-sizer',
      transitionDuration: '0.4s',
      stagger: 30,
      percentPosition: true
    }"
    @layoutComplete="doStuff();"
    ref="dashboard"
  >
    <div class="grid-sizer"></div>
    <div class="gutter-sizer"></div>

    <dashboard-item
      v-for="item in items"
      class="dashboard-item"
      :key="item.order"
      :title="item.title"
      :img="item.tempImgURL"
      :data-packery="{
        columns: item.columns,
        rows: item.rows
      }"
      v-packery-item="{ draggable: true }"
      @dragEnd="doStuff();"
    >
      <component v-if="item.component" v-bind:is="item.component" />
    </dashboard-item>
  </section>
</template>

<script>
//v-draggabilly
import DashboardItem from "./DashboardItem";
import Assets from "./Subcomponents/Assets";
import { packeryEvents } from "vue-packery-plugin";

export default {
  name: "Dashboard",
  components: {
    DashboardItem
  },
  ready: function() {},
  methods: {
    doStuff: function() {
      packeryEvents.$emit("layout", this.$el);
      //$(window).trigger("resize");
      console.log("Packery!");
      console.log([this.$el]);
    },
    reLayout: function() {
      console.log(this.$refs.dashboard);
    }
  },
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      items: [
        {
          order: 1,
          title: "Assets",
          slug: "assets",
          component: Assets,
          //tempImgURL: "https://i.ibb.co/z5cwwcH/1-assets-2x.png",
          columns: 1,
          rows: 2
        },
        {
          order: 2,
          title: "Gap Analysis",
          slug: "gap-analysis",
          tempImgURL: "https://i.ibb.co/xDDcSYS/2-gap-2x.png",
          columns: 1,
          rows: 2
        },
        {
          order: 3,
          title: "Controls",
          slug: "controls",
          tempImgURL: "https://i.ibb.co/1by70B5/3-controls-2x.png",
          columns: 2,
          rows: 1
        },
        {
          order: 4,
          title: "Clauses",
          slug: "clauses",
          tempImgURL: "https://i.ibb.co/ck3TvzC/4-clauses-2x.png",
          columns: 2,
          rows: 1
        }
      ]
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
* {
  box-sizing: border-box;
}
$gap: 2%;
$columnQuarter: 23%;
$columnThird: 31%;
$columnHalf: ($columnQuarter * 2) + $gap;
$columnFull: ($columnQuarter * 4) + ($gap * 3);
.gutter-sizer {
  width: $gap;
}

html {
  overflow-y: scroll;
}
body {
  padding: $gap;
  background-color: gainsboro;
}

.dashboard {
  &:after {
    content: "";
    display: block;
    clear: both;
  }
}

.grid-sizer,
.dashboard-item,
[data-columns="1"] {
  width: $columnQuarter;
}

.dashboard-item {
  float: left;
  img {
    width: 100%;
  }
}
[data-columns="1"] {
  width: $columnQuarter;
}
[data-columns="2"] {
  width: $columnHalf;
}
[data-columns="4"] {
  width: $columnFull;
}

@media (max-width: 1024px) {
  //.dashboard-item { width: $columnThird; }
}

@media (max-width: 980px) {
  .dashboard-item {
    width: $columnHalf !important;
  }
}
@media (max-width: 480px) {
  .dashboard-item {
    width: $columnFull !important;
  }
}

.dashboard-item.is-dragging,
.dashboard-item.is-positioning-post-drag {
  background: blue;
  z-index: 2; /* keep dragged item on top */
}
.packery-drop-placeholder {
  outline: 3px dashed #444;
  outline-offset: -6px;
  /* transition position changing */
  transition: transform 0.2s;
}

/** Button Code **/

.button {
  width: 72px;
  height: 72px;
  line-height: 72px;
  display: block;
  position: relative;
  -moz-border-radius: 50%;
  -webkit-border-radius: 50%;
  border-radius: 50%;
  border: 2px solid #444;
  text-align: center;
  display: inline-block;
  vertical-align: middle;
  position: relative;
  z-index: 10;
  color: #333;
  opacity: 0.2;

  position: fixed;
  top: 0.5em;
  right: 0.5em;
  transform: scale(0.5);
  cursor: pointer !important;
  font-size: 30px;

  &:hover {
    opacity: 1;
  }
}

.button:after {
  position: absolute !important;
  content: "";
  width: 56px;
  height: 56px;
  display: block;
  position: relative;
  -moz-border-radius: 50%;
  -webkit-border-radius: 50%;
  border-radius: 50%;
  right: 50%;
  top: 50%;
  background-color: #333;
  visibility: hidden;
  opacity: 0;
  opacity: 1\9;
  visibility: visible\9;
  display: none\9;
  transform: scale(0.5, 0.5) translate(50%, -50%);
  z-index: -1;
}

.button:hover:after {
  visibility: visible;
  opacity: 0.2;
  display: block\9;
  transform: scale(1, 1) translate(50%, -50%);
}
</style>
