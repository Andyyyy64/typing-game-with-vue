<script>
export default {
  data() {
    return {
      startFlg: "",
      current_question: "",
      questions: [
        "apple",
        "banana",
        "chocolate",
        "donut",
        "espresso"
      ],
      typeBox: "",
      current_question_counts: 0,
      question_counts: 0,
    }
  },
  methods: {
    gameStart() {
      this.startFlg = true
      this.$nextTick(function () {
        document.getElementById("typeForm").focus()
      })
    }
  },
  mounted() {
    this.current_question = this.questions[0]
    this.question_counts = this.questions.length
  },
  watch: {
    typeBox(e) {
      if (e == this.current_question) {
        this.questions.splice(0, 1)
        this.current_question = this.questions[0]
        this.typeBox = ""
        this.current_question_counts = this.current_question_counts + 1
      }
    }
  },
  computed: {
    styleobject() {
      var width = 20 * this.current_question_counts + "%"
      if (this.current_question_counts == 5) {
        var color = "#03a9f4"
      } else {
        color = "orange"
      }
      return {
        "width": width,
        "background-color": color
      }
    },
  }
}
</script>


<template>
  <div class="contaier">
    <div class="title">
      <h1>Typing Game</h1>
      <div class="marker"></div>
    </div>
    <button v-if="!startFlg" @click="gameStart" class="startbutton mb-20">START</button>
    <div v-if="startFlg">
      <div class="question">{{ current_question }}</div>
      <div v-if="current_question_counts == question_counts" class="clear">Clear!</div>
      <div class="typeFormWrapper mb-20">
        <input id="typeForm" v-model="typeBox" type="text" class="typeForm">
      </div>

      <div class="gaugeWrapper">
        <div :style="styleobject" class="gauge"></div>
      </div>
      <div>{{ current_question_counts }}/{{ question_counts }}</div>
    </div>
  </div>
</template>

<style>
* {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}

template {
  font-size: 32px;
}

.mb-20 {
  margin-bottom: 20px;
}

.contaier {
  width: 400px;
  margin: 0 auto;
  text-align: center;
}

.title {
  position: relative;
  font-size: 48px;
}

.marker {
  width: 100%;
  height: 35%;
  background-color: #a2a2a270;
  position: absolute;
  bottom: 5%;
  z-index: -1;
}

.startbutton {
  background-color: #333;
  color: #fff;
  padding: 4px 60px;
  border: none;
  outline: none;
  border-radius: 8px;
  cursor: pointer;
}

.startbutton:hover {
  opacity: 0.7;
}

.question {
  color: black;
}

.clear {
  color: #03a9f3;
}

.typeForm {
  text-align: center;
  outline: none;
  border: none;
}

.typeFormWrapper {
  border-bottom: 1px solid gray;
}

.gauge {
  height: 12px;
}

.gaugeWrapper {
  border: 1px solid;
  height: 12px;
}
</style>