<template>
  <div class="selectBox">
    <div class="showBox" @click="showOption"></div>
    <ul v-show="flag" class="optionsBox" :style="{height:hgt}">
      <li v-for="(item,key) in info" :key="key" @click="confirmData">{{item}}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "my-select",
    data: function () {
      return {
        flag: false
      }
    },
    props: {
      info: {
        type: Array,
        default: []
      },
      hgt: {
        type: String,
        default: ""
      }
    },
    methods: {
      showOption: function () {
        let evt = event.target;
        if (this.flag) {
          this.flag = false;
          evt.setAttribute("class", "showBox");
        } else {
          this.flag = true;
          evt.setAttribute("class", "showBox showBoxF");
        }
      },
      confirmData: function () {
        let evt = event.target;
        let showBox = document.getElementsByClassName("showBox")[0];
        let str = showBox.innerText;
        if (str != evt.innerText) {
          showBox.innerText = evt.innerText;
          showBox.setAttribute("class", "showBox");
          this.flag = false;
          this.$emit("changeEvent", evt.innerText);
        }
      }
    },
    mounted: function () {
      let showBox = document.getElementsByClassName("showBox")[0];
      showBox.innerText = this.info[0] ? this.info[0] : "";
    }
  }
</script>

<style scoped>

  *{
    outline: none;
  }

  .selectBox {
    display: inline-block;
    position: relative;
    min-width: 150px;
  }

  .showBox {
    width: 100%;
    text-align: left;
    position: relative;
    overflow: hidden;
    padding: 5px 10px 3px;
    border: 1px solid #9d9d9d;
    border-radius: 4px;
    box-sizing: border-box;
    color: #6d6d6d;
    cursor: pointer;
  }

  .optionsBox {
    position: absolute;
    left: 0;
    background-color: #fff;
    /*top: 0;*/
    list-style: none;
    /*display: inline-block;*/
    border: 1px solid #bbbbbb;
    border-radius: 1px;
    margin-top: 3px;
    padding: 0;
    z-index: 1;
    overflow-y: auto;
  }

  .optionsBox li {
    padding: 5px 10px;
    background-color: #fff;
    color: #7d7d7d;
    cursor: pointer;
    border-radius: 4px;
  }

  .optionsBox li + li {
    border-top: 1px dotted #b2bbc6;
  }

  .optionsBox li:hover {
    background-color: #7d7d7d;
    color: #fff;
    transition: all 0.3s;
  }

  .showBox:after {
    display: inline-block;
    content: 'ㄑ';
    clear: both;
    transform: rotate(-90deg);
    float:right;
    margin-left: 10px;
    transition: all .2s;
  }

  .showBoxF:after {
    transform: rotate(-270deg);
    transition: all .5s;
  }
  ::-webkit-scrollbar {
    width: 14px;
    height: 14px;
  }

  ::-webkit-scrollbar-track,
  ::-webkit-scrollbar-thumb {
    border-radius: 999px;
    border: 5px solid transparent;
  }

  ::-webkit-scrollbar-track {
    box-shadow: 1px 1px 5px rgba(0,0,0,.2) inset;
  }

  ::-webkit-scrollbar-thumb {
    min-height: 20px;
    background-clip: content-box;
    box-shadow: 0 0 0 5px rgba(0,0,0,.2) inset;
  }

  ::-webkit-scrollbar-corner {
    background: transparent;
  }
</style>
