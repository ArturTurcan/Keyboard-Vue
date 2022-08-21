<template>
  <div  class="keyboard">
    <div :class="element.divClass" v-for="element in elements">
      <ul  :class="element.ulClass">
        <li  v-for="li in element.buttons" :class="li.liClass.concat(li.id === selectedElement ? ' newClass' : '')" :ref="li.id"> {{ li.label }}</li>
      </ul>
    </div>
  </div>
</template>
<script>

const elements = [
  {
    divClass: "line__one", ulClass: "row row-one", buttons: [
      {liClass: "bordo", id: "Escape", label:"ESC"},
      {liClass: "bordo", id: "Digit1", label:"1"},
      {liClass: "red-pink", id: "Digit2", label:"2"},
      {liClass: "orange", id: "Digit3", label:"3"},
      {liClass: "yellow", id: "Digit4", label:"4"},
      {liClass: "green-yellow", id: "Digit5", label:"5"},
      {liClass: "green-yellow", id: "Digit6", label:"6"},
      {liClass: "yellow", id: "Digit7", label:"7"},
      {liClass: "orange", id: "Digit8", label:"8"},
      {liClass: "red-pink", id: "Digit9", label:"9"},
      {liClass: "bordo", id: "Digit0", label:"0"},
      {liClass: "bordo", id: "Minus", label:"-"},
      {liClass: "bordo", id: "Equal", label:"="},
      {liClass: "bordo", id: "Backspace", label:"backSpace"},
    ]
  },
  {
    divClass: "line__two", ulClass: "row row-two", buttons: [
      {liClass: "bordo", id: "Tab", label:"Tab"},
      {liClass: "bordo", id: "KeyQ", label:"Q"},
      {liClass: "red-pink", id: "KeyW", label:"W"},
      {liClass: "orange", id: "KeyE", label:"E"},
      {liClass: "yellow", id: "KeyR", label:"R"},
      {liClass: "green-yellow", id: "KeyT", label:"T"},
      {liClass: "green-yellow", id: "KeyY", label:"Y"},
      {liClass: "yellow", id: "KeyU", label:"U"},
      {liClass: "orange", id: "KeyI", label:"I"},
      {liClass: "red-pink", id: "KeyO", label:"O"},
      {liClass: "bordo", id: "KeyP", label:"P"},
      {liClass: "bordo", id: "BracketLeft", label:"["},
      {liClass: "bordo", id: "BracketRight", label:"]"},
      {liClass: "bordo", id: "Backslash", label:"|"},
    ]
  },
  {
    divClass: "line__three", ulClass: "row row-three", buttons: [
      {liClass: "bordo", id: "CapsLock", label:"CapsLock"},
      {liClass: "bordo", id: "KeyA", label:"A"},
      {liClass: "red-pink", id: "KeyS", label:"S"},
      {liClass: "orange", id: "KeyD", label:"D"},
      {liClass: "yellow", id: "KeyF", label:"F"},
      {liClass: "green-yellow", id: "KeyG", label:"G"},
      {liClass: "green-yellow", id: "KeyH", label:"H"},
      {liClass: "yellow", id: "KeyJ", label:"J"},
      {liClass: "orange", id: "KeyK", label:"K"},
      {liClass: "red-pink", id: "KeyL", label:"L"},
      {liClass: "bordo", id: "Semicolon", label:";"},
      {liClass: "bordo", id: "Quote", label:"'"},
      {liClass: "bordo", id: "Enter", label:"Enter"},
    ]
  }, {
    divClass: "line__four", ulClass: "row row-four", buttons: [
      {liClass: "bordo", id: "ShiftLeft", label:"ShiftLeft"},
      {liClass: "bordo", id: "KeyZ", label:"Z"},
      {liClass: "red-pink", id: "KeyX", label:"X"},
      {liClass: "orange", id: "KeyC", label:"C"},
      {liClass: "yellow", id: "KeyV", label:"V"},
      {liClass: "green-yellow", id: "KeyB", label:"B"},
      {liClass: "green-yellow", id: "KeyN", label:"N"},
      {liClass: "yellow", id: "KeyM", label:"M"},
      {liClass: "orange", id: "Comma", label:"<"},
      {liClass: "red-pink", id: "Period", label:">"},
      {liClass: "bordo", id: "Slash", label:"?"},
      {liClass: "bordo", id: "ShiftRight", label:"ShiftRight"},
    ]
  }, {
    buttons: [
      {liClass: "row space", id: "Space", label: "SPACE"},
    ]
  },
]
export default {
  name: 'App',
  components: {  },
  data() {
    return {
      selectedElement: '',
      counterTrue: 0,
      counterFalse: 0,
      elements
    }
  },
  methods: {
    pressKey(code){
      this.$refs[code][0].classList.add("selected")
      setTimeout(() => this.$refs[code][0].classList.remove("selected"), 1000)
    },
    keydown(e){
      this.pressKey(e.code)
      if (e.code === this.selectedElement){
        this.getRandomElementFromArr()
      }
    },
    getRandomElementFromArr() {
      this.$nextTick(()=> {
        const keys = Object.keys(this.$refs)
      this.selectedElement = keys[Math.floor(Math.random() * keys.length)]
      })
    }
  },
  mounted() {
    window.addEventListener("keydown", this.keydown)
    this.getRandomElementFromArr()
  }
}
</script>

<style>
body {
  background-color: black;
  padding-top: 150px;
  padding-right: 100px;
  padding-left: 100px;
}

.space {
  background-color: darkred;
  animation: vibrate-1 0.3s linear infinite both;
}

.keyboard {
  display: flex;
  flex-direction: column;
}

li {
  border: 1px solid red;
  border-radius: 7px;
  padding: 15px 20px;
  list-style: none;
}

.row {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

.bordo {
  background-color: darkred;
}

.red-pink {
  background-color: indianred;
}

.orange {
  background-color: orangered;
}

.yellow {
  background-color: yellow;
}

.green-yellow {
  background-color: greenyellow;
}

.newClass {
  background-color: deeppink;
  -webkit-animation: vibrate-1 0.3s linear infinite both;
  animation: vibrate-1 0.3s linear infinite both;
  color: white;
}

.selected {
  transition: all 3.2s ease;
  transform: rotate(9000deg) scale(1);
  background-color: white;
  color: red;
}

.hit {
  -webkit-animation: hit 0.3s cubic-bezier(0.390, 0.575, 0.565, 1.000) both;
  animation: hit 0.3s cubic-bezier(0.390, 0.575, 0.565, 1.000) both;
}

@-webkit-keyframes hit {
  0% {
    -webkit-transform: scale(1.2);
    transform: scale(1.2);
  }
  100% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}

@keyframes hit {
  0% {
    -webkit-transform: scale(1.2);
    transform: scale(1.2);
  }
  100% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}


@keyframes vibrate-1 {
  0% {
    -webkit-transform: translate(0);
    transform: translate(0);
  }
  20% {
    -webkit-transform: translate(-2px, 2px);
    transform: translate(-2px, 2px);
  }
  40% {
    -webkit-transform: translate(-2px, -2px);
    transform: translate(-2px, -2px);
  }
  60% {
    -webkit-transform: translate(2px, 2px);
    transform: translate(2px, 2px);
  }
  80% {
    -webkit-transform: translate(2px, -2px);
    transform: translate(2px, -2px);
  }
  100% {
    -webkit-transform: translate(0);
    transform: translate(0);
  }
}
</style>
