<template>
  <div id="main">
    <nav>
      <div class="left">
        <div class="middle">
          <div class="wrapper">
            <div class="alpha">
              <h1 class="title">선린급식</h1>
              <div class="date">{{date}}</div>
            </div>
            <div class="content" @click="first()">
              <h2>오늘</h2>
              <div
                class="todLunch"
              >{{tod[0]}} {{tod[1]}} {{tod[2]}} {{tod[3]}} {{tod[4]}} {{tod[5]}}</div>
              <div class="like">
                <div class="wrap">
                  <img src="smile.png" alt="good" class="img" />
                  {{good1}}
                </div>
                <div class="wrap">
                  <img src="soso.png" alt="soso" class="img" />
                  {{soso1}}
                </div>
                <div class="wrap">
                  <img src="angry.png" alt="angry" class="img" />
                  {{angry1}}
                </div>
              </div>
            </div>
            <div class="content" @click="second()">
              <h2>내일</h2>
              <div
                class="todLunch"
              >{{tom[0]}} {{tom[1]}} {{tom[2]}} {{tom[3]}} {{tom[4]}} {{tom[5]}}</div>
              <div class="like">
                <div class="wrap">
                  <img src="smile.png" alt="good" class="img" />
                  {{good2}}
                </div>
                <div class="wrap">
                  <img src="soso.png" alt="soso" class="img" />
                  {{soso2}}
                </div>
                <div class="wrap">
                  <img src="angry.png" alt="angry" class="img" />
                  {{angry2}}
                </div>
              </div>
            </div>
            <div class="content" @click="third()">
              <h2>모레</h2>
              <div
                class="todLunch"
              >{{tomm[0]}} {{tomm[1]}} {{tomm[2]}} {{tomm[3]}} {{tomm[4]}} {{tomm[5]}}</div>
              <div class="like">
                <div class="wrap">
                  <img src="smile.png" alt="good" class="img" />
                  {{good3}}
                </div>
                <div class="wrap">
                  <img src="soso.png" alt="soso" class="img" />
                  {{soso3}}
                </div>
                <div class="wrap">
                  <img src="angry.png" alt="angry" class="img" />
                  {{angry3}}
                </div>
              </div>
            </div>
          </div>
          <chartjs-doughnut
            v-bind:labels="labels"
            v-bind:datasets="datasets"
            v-bind:option="option"
          ></chartjs-doughnut>
        </div>
      </div>
      <div id="myModal" class="modal">
        <div class="modal-content">
          <span class="close" @click="sdfg()">&times;</span>
          <div id="one">
            <h2 style="margin-left: 100px; font-size: 2em;">오늘</h2>
            <br />
            <div style="display: flex; width: 100%; justify-content: space-around;">
              <img src="smile.png" alt class="imger" @click="todsel(1)" />
              <img src="soso.png" alt class="imger" @click="todsel(2)" />
              <img src="angry.png" alt class="imger" @click="todsel(3)" />
            </div>
          </div>
          <div id="two">
            <h2 style="margin-left: 100px; font-size: 2em;">내일</h2>
            <br />
            <div style="display: flex; width: 100%; justify-content: space-around;">
              <img src="smile.png" alt class="imger" @click="todsel(4)" />
              <img src="soso.png" alt class="imger" @click="todsel(5)" />
              <img src="angry.png" alt class="imger" @click="todsel(6)" />
            </div>
          </div>
          <div id="three">
            <h2 style="margin-left: 100px; font-size: 2em;">모레</h2>
            <br />
            <div style="display: flex; width: 100%; justify-content: space-around;">
              <img src="smile.png" alt class="imger" @click="todsel(7)" />
              <img src="soso.png" alt class="imger" @click="todsel(8)" />
              <img src="angry.png" alt class="imger" @click="todsel(9)" />
            </div>
          </div>
          <div
            style="width: 100%; z-index: 1000; display: flex; justify-content: center; align-items: cneter,padding: 50px"
          >
            <span
              class="btn"
              @click="sdfg()"
              style="margin-top: 20px;border: 1px solid gray; padding: 10px 10px; border-radius: 20px;"
            >급식 투표하기</span>
          </div>
        </div>
      </div>
      <div class="right"></div>
    </nav>
    <button>
      <span class="btn" id="myBtn" @click="asdf()">급식 투표하기</span>
    </button>
  </div>
</template>
<script>
import Router from "../router/index";
import axios from "axios";
import cheerio from "cheerio";

export default {
  data() {
    return {
      lunch: [],
      tod: [],
      tom: [],
      tomm: [],
      date: "",
      good1: 0,
      good2: 0,
      good3: 0,
      soso1: 0,
      soso2: 0,
      soso3: 0,
      angry1: 0,
      angry2: 0,
      angry3: 0,
      labels: ["good", "Not bad", "Angry"],
      datasets: [
        {
          data: [
            this.$store.state.todgood,
            this.$store.state.todsoso,
            this.$store.state.todangry
          ],
          backgroundColor: ["#6dd900", "#ffda47", "#ff2626"]
        }
      ],
      option: {
        title: {
          display: true,
          text: "TODAY",
          width: "30vw"
        }
      }
    };
  },
  methods: {
    first() {
      var x = this.$store.state;
      this.datasets[0].data[0] = x.todgood;
      this.datasets[0].data[1] = x.todsoso;
      this.datasets[0].data[2] = x.todangry;
      this.option.title.text = "TODAY";
    },
    second() {
      console.log("1");
      this.datasets[0].data[0] = x.tomgood;
      this.datasets[0].data[1] = x.tomsoso;
      this.datasets[0].data[2] = x.tomangry;
      this.option.title.text = "TOMMOROW";
    },
    third() {
      this.datasets[0].data[0] = x.tommgood;
      this.datasets[0].data[1] = x.tommsoso;
      this.datasets[0].data[2] = x.tommangry;
      this.option.title.text = "THE DAY AFTER TOMMOROW";
    },
    asdf() {
      var modal = document.getElementById("myModal");
      modal.style.display = "block";
    },
    sdfg() {
      var x = this.$store.state;
      var modal = document.getElementById("myModal");
      modal.style.display = "none";
      this.good1 = x.todgood;
      this.good2 = x.tomgood;
      this.good3 = x.tommgood;
      this.soso1 = x.todsoso;
      this.soso2 = x.tomsoso;
      this.soso3 = x.tommsoso;
      this.angry1 = x.todangry;
      this.angry2 = x.tomangry;
      this.angry3 = x.tommangry;
      document.getElementById("one").style.display = "block";
      document.getElementById("two").style.display = "block";
      document.getElementById("three").style.display = "block";
    },
    todsel(el) {
      var x = this.$store.state;
      if (el == 1) {
        x.todgood += 1;
        document.getElementById("one").style.display = "none";
      }
      if (el == 2) {
        x.todsoso += 1;
        document.getElementById("one").style.display = "none";
      }
      if (el == 3) {
        x.todangry += 1;
        document.getElementById("one").style.display = "none";
      }
      if (el == 4) {
        x.tomgood += 1;
        document.getElementById("two").style.display = "none";
      }
      if (el == 5) {
        x.tomsoso += 1;
        document.getElementById("two").style.display = "none";
      }
      if (el == 6) {
        x.tomangry += 1;
        document.getElementById("two").style.display = "none";
      }
      if (el == 7) {
        x.tommgood += 1;
        document.getElementById("three").style.display = "none";
      }
      if (el == 8) {
        x.tommsoso += 1;
        document.getElementById("three").style.display = "none";
      }
      if (el == 9) {
        x.tommangry += 1;
        document.getElementById("three").style.display = "none";
      }
    }
  },

  created() {
    axios
      .get("http://sunrint.hs.kr/index.do#none")
      .then(data => {
        var $ = cheerio.load(data.data);
        $("p.menu").each((idx, ele) => {
          var x = [];
          x.push(ele.children[0].data);
          console.log(x);
          this.lunch.push(x[0].trim());
          console.log(this.lunch[0]);
        });
      })
      .then(() => {
        var k = this.lunch[0];
        var str = k.split("\n");
        var str2 = str[0].split(",");
        this.tod = str2;
        var k2 = this.lunch[1];
        var str1 = k2.split("\n");
        var str21 = str1[0].split(",");
        this.tom = str21;
        var k3 = this.lunch[2];
        var str222 = k3.split("\n");
        var str22 = str222[0].split(",");
        this.tomm = str22;
        this.$store.state.tod = this.tod;
        this.$store.state.tom = this.tom;
        this.$store.state.tomm = this.tomm;
      });
    var x = new Date();
    this.date = x.toLocaleDateString();
  },
  mounted() {
    document.getElementsByTagName("canvas")[0].style.height = "45vw";
    document.getElementsByTagName("canvas")[0].style.width = "45vw";
    document.getElementsByTagName("canvas")[0].style.position = "relative";
    document.getElementsByTagName("canvas")[0].style.top = "30vh";
  }
};
</script>


<style scoped>
nav {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: space-between;
}
.left {
  width: 85vw;
  height: 100vh;
  background: white;
  box-sizing: content-box;
  justify-content: center;
}
.right {
  width: 15vw;
  height: 100%;
  background: #111;
}
.title {
  font-size: 4em;
  font-weight: bold;
  margin-bottom: 3vh;
}
.date {
  font-size: 2.5em;
}
.alpha {
  margin-bottom: 20px;
}
.middle {
  margin: 2vh auto;
  display: flex;
  flex-flow: row;
}
.content {
  display: flex;
  flex-flow: column;
  margin: 1.5vh 0;
  width: 35vw;
  transition-duration: 444ms;
  border: 1px solid gray;
  padding: 10px;
  cursor: pointer;
}
.chartjs-render-monitor {
  width: 1000px;
  height: 1000px;
}
.content:hover {
  box-shadow: 10px 10px 5px 0px rgba(0, 0, 0, 0.75);
}
.like {
  margin-top: 10px;
  text-align: right;
  display: flex;
  justify-content: flex-end;
}
.img {
  width: 3em;
  margin-right: 8px;
}
.wrap {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-right: 15px;
  font-size: bold;
}
.test {
  position: absolute;
  width: 60vw;
  height: 80vh;
  position: fixed;
}
.wrapper {
  display: flex;
  flex-flow: column;
  margin-left: 10vw;
  width: 50vw;
}
button {
  position: absolute;
  right: 16vw;
  bottom: 10px;
  outline: none;
  text-decoration: none;
  border-radius: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  text-transform: uppercase;
  height: 60px;
  width: 210px;
  opacity: 1;
  background-color: #ffffff;
  border: 1px solid rgba(22, 76, 167, 0.6);
}
.btn {
  color: rgba(22, 76, 167, 1);
  font-size: 17px;
  font-weight: 500;
  letter-spacing: 0.7px;
}
.btn:hover {
  animation: storm 0.7s ease-in-out both;
  animation-delay: 0.06s;
  animation: rotate 0.7s ease-in-out both;
}
button:hover {
  animation: rotate 0.7s ease-in-out both;
}

@keyframes rotate {
  0% {
    transform: rotate(0deg) translate3d(0, 0, 0);
  }

  25% {
    transform: rotate(3deg) translate3d(0, 0, 0);
  }

  50% {
    transform: rotate(-3deg) translate3d(0, 0, 0);
  }

  75% {
    transform: rotate(1deg) translate3d(0, 0, 0);
  }

  100% {
    transform: rotate(0deg) translate3d(0, 0, 0);
  }
}

@keyframes storm {
  0% {
    transform: translate3d(0, 0, 0) translateZ(0);
  }

  25% {
    transform: translate3d(4px, 0, 0) translateZ(0);
  }

  50% {
    transform: translate3d(-3px, 0, 0) translateZ(0);
  }

  75% {
    transform: translate3d(2px, 0, 0) translateZ(0);
  }

  100% {
    transform: translate3d(0, 0, 0) translateZ(0);
  }
}
.modal {
  display: none;
  position: fixed;
  z-index: 1;
  padding-top: 100px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  height: 80%;
}

.close {
  color: #aaaaaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}
.imger {
  margin: 0 10px;
}
</style>
