<template>
    <head>
        <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Source+Sans+Pro:300">
        <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.4.1/css/all.css" integrity="sha384-5sAR7xN1Nv6T6+dT2mhtzEpVJvfS3NScPQTrOxhwjIuvcA67KV2R5Jz6kr4abQsz" crossorigin="anonymous">
        <link rel="stylesheet" href="stopWatch.css">
    </head>
    <div class="outside-container">
        <div id="switch-container">
            <label class="switch">
                <input type="checkbox" v-on:click="switchPages()">
                <span class="slider round"></span>
                <p id="slider-text" style="color: white; font-weight: bold;">Scores</p>
            </label>
        </div>
        <div id="page-one">
            <div class="wrapper">
                <div class="typing-demo" style="color: white;">
                {{name}}
                </div>
            </div>
            <div class="button-container">
                    <button v-if="date.getDay() == 1" v-on:click="threeRandomInts = getThreeRandomUniqueIntsInRange(0, objects.length-1)">
                        Get Monday Words
                    </button>
                    <button v-if="date.getDay() == 2" v-on:click="threeRandomInts = getThreeRandomUniqueIntsInRange(0, personplaceanimal.length-1)">
                        Get Tuesday Words
                    </button>
                    <button v-if="date.getDay() == 3" v-on:click="threeRandomInts = getThreeRandomUniqueIntsInRange(0, actions.length-1)">
                        Get Wednesday Words
                    </button>
                    <button v-if="date.getDay() == 4" v-on:click="threeRandomInts = getThreeRandomUniqueIntsInRange(0, difficult.length-1)">
                        Get Thursday Words
                    </button>
                    <button v-if="date.getDay() == 5" v-on:click="threeRandomInts = getThreeRandomUniqueIntsInRange(0, popculture.length-1)">
                        Get Friday Words
                    </button>
            </div>
            <div id="word-container">
                <div id="Monday" v-if="date.getDay() == 1"> <!-- Monday -->
                    <p>{{objects[threeRandomInts[0]]}}</p>
                    <p>{{objects[threeRandomInts[1]]}}</p>
                    <p>{{objects[threeRandomInts[2]]}}</p>
                </div>
                <div id="Tuesday" v-if="date.getDay() == 2"> <!-- Tuesday -->
                    <p>{{personplaceanimal[threeRandomInts[0]]}}</p>
                    <p>{{personplaceanimal[threeRandomInts[1]]}}</p>
                    <p>{{personplaceanimal[threeRandomInts[2]]}}</p>
                </div>
                <div id="Wednesday" v-if="date.getDay() == 3"> <!-- Wednesday -->
                    <p>{{actions[threeRandomInts[0]]}}</p>
                    <p>{{actions[threeRandomInts[1]]}}</p>
                    <p>{{actions[threeRandomInts[2]]}}</p>
                </div>
                <div id="Thursday" v-if="date.getDay() == 4"> <!-- Thursday -->
                    <p>{{difficult[threeRandomInts[0]]}}</p>
                    <p>{{difficult[threeRandomInts[1]]}}</p>
                    <p>{{difficult[threeRandomInts[2]]}}</p>
                </div>
                <div id="Friday" v-if="date.getDay() == 5"> <!-- Friday -->
                    <p>{{popculture[threeRandomInts[0]]}}</p>
                    <p>{{popculture[threeRandomInts[1]]}}</p>
                    <p>{{popculture[threeRandomInts[2]]}}</p>
                </div>
            </div>
            <div id="timerContainer">
                <div class="timer" v-on:click="startTimer()">Start Timer!</div>
                <div class="startTimer reset" v-on:click="startTimer()" >
                    <i class="fas fa-play"></i>
                </div>
                <div class="pauseTimer reset" v-on:click="pauseTimer()" >
                    <i class="fas fa-pause"></i>
                </div>
                <div class="resetTimer reset" v-on:click="resetTimer()">Reset</div>
            </div>
        </div>
        <div id="page-two" hidden>
            <h3 style="@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap'); 
            font-family: 'Bebas Neue', cursive; font-size: 3.5rem; margin-top: 0; color: black; background-color: white; width: 250px;
            display: inline-block; box-shadow: 2px 2px 2px black;">Scores</h3>
            <p style="color: white; font-weight: bold; font-size: 2rem;">Overall</p>
            <table>
            <tr>
                <th>{{scores[0].Name}}</th>
                <th>{{scores[1].Name}}</th>
                <th>{{scores[2].Name}}</th>
                <th>{{scores[3].Name}}</th>
                <th>{{scores[4].Name}}</th>
            </tr>
            <tr>
                <td>{{scores[0].Score}}</td>
                <td>{{scores[1].Score}}</td>
                <td>{{scores[2].Score}}</td>
                <td>{{scores[3].Score}}</td>
                <td>{{scores[4].Score}}</td>
            </tr>
            <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true" v-on:click="addToJSONScores(0)"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true" v-on:click="addToJSONScores(1)"></i>
                    </button>
                </td>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true" v-on:click="addToJSONScores(2)"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true" v-on:click="addToJSONScores(3)"></i>
                    </button>
                </td>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true"></i>
                    </button>
                </td>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true"></i>
                    </button>
                </td>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true"></i>
                    </button>
                </td>
            </table>
            <p style="color: white; font-weight: bold; font-size: 2rem; margin-top: 75px;">Weekly</p>
            <table>
            <tr>
                <th>{{scores[5].Name}}</th>
                <th>{{scores[6].Name}}</th>
                <th>{{scores[7].Name}}</th>
                <th>{{scores[8].Name}}</th>
                <th>{{scores[9].Name}}</th>
            </tr>
            <tr>
                <td>{{scores[5].Score}}</td>
                <td>{{scores[6].Score}}</td>
                <td>{{scores[7].Score}}</td>
                <td>{{scores[8].Score}}</td>
                <td>{{scores[9].Score}}</td>
            </tr>
            <tr>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true"></i>
                    </button>
                </td>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true"></i>
                    </button>
                </td>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true"></i>
                    </button>
                </td>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true"></i>
                    </button>
                </td>
                <td>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-minus" aria-hidden="true"></i>
                    </button>
                    <button type="button" class="button hollow circle" data-quantity="minus" data-field="quantity">
                        <i class="fa fa-plus" aria-hidden="true"></i>
                    </button>
                </td>
            </tr>
            </table>
        </div>
    </div>
    <div>
        <Data />
    </div>
</template>

<script>
import Data from './Data.vue'
    export default {
        data () {
            return {
                name: "TMC Pictionary",
                objects: require('../../data/objects.json'),
                actions: require('../../data/action.json'),
                personplaceanimal: require('../../data/personplaceanimal.json'),
                popculture: require('../../data/popculture.json'),
                difficult: require('../../data/difficult.json'),
                scores: require('../../data/scores.json'),
                date: new Date(),
                threeRandomInts: [],
                startTime: 0,
                updatedTime: 0,
                difference: 0,
                tInterval: 0,
                savedTime: 0,
                paused: 0,
                running: 0,
                pageOne: true,
                info: [],
            }
        },
        methods: {
            getThreeRandomUniqueIntsInRange(min, max) {
                var vals = [];
                var value = 0;
                min = Math.ceil(min);
                max = Math.floor(max);
                for(var i = 0; i < 3; i++) {
                    value = Math.floor(Math.random() * (max - min + 1) + min);
                    if(!vals.includes(value)) {
                        vals.push(value); 
                    } else {
                        i--;
                    }
                }
                return vals;
            },
            startTimer(){
                document.getElementsByClassName("timer").innerHTML = "hi";
                if(!this.running){
                    this.startTime = new Date().getTime();
                    this.tInterval = setInterval(this.getShowTime, 1);
                // change 1 to 1000 above to run script every second instead of every millisecond. one other change will be needed in the getShowTime() function below for this to work. see comment there.   
                
                    this.paused = 0;
                    this.running = 1;
                    document.querySelector('.timer').style.background = "#FF0000";
                    document.querySelector('.timer').style.cursor = "auto";
                    document.querySelector('.timer').style.color = "yellow";
                    document.querySelector('.startTimer').classList.add('lighter');
                    document.querySelector('.pauseTimer').classList.remove('lighter');
                    document.querySelector('.startTimer').style.cursor = "auto";
                    document.querySelector('.pauseTimer').style.cursor = "pointer";
                }
            },
            pauseTimer(){
                if (!this.difference){
                    // if timer never started, don't allow pause button to do anything
                } else if (!this.paused) {
                    clearInterval(this.tInterval);
                    this.savedTime = this.difference;
                    this.paused = 1;
                    this.running = 0;
                    document.querySelector('.timer').style.background = "#A90000";
                    document.querySelector('.timer').style.color = "#690000";
                    document.querySelector('.timer').style.cursor = "pointer";
                    document.querySelector('.startTimer').classList.remove('lighter');
                    document.querySelector('.pauseTimer').classList.add('lighter');
                    document.querySelector('.startTimer').style.cursor = "pointer";
                    document.querySelector('.pauseTimer').style.cursor = "auto";
                } else {
                // if the timer was already paused, when they click pause again, start the timer again
                this.startTimer();
                }
            },
            resetTimer(){
                clearInterval(this.tInterval);
                this.savedTime = 0;
                this.difference = 0;
                this.paused = 0;
                this.running = 0;
                document.querySelector('.timer').innerHTML = 'Start Timer!';
                document.querySelector('.timer').style.background = "#A90000";
                document.querySelector('.timer').style.color = "#fff";
                document.querySelector('.timer').style.cursor = "pointer";
                document.querySelector('.startTimer').classList.remove('lighter');
                document.querySelector('.pauseTimer').classList.remove('lighter');
                document.querySelector('.startTimer').style.cursor = "pointer";
                document.querySelector('.pauseTimer').style.cursor = "auto";
            },
            getShowTime(){
                this.updatedTime = new Date().getTime();
                if (this.savedTime){
                    this.difference = (this.updatedTime - this.startTime) + this.savedTime;
                } else {
                    this.difference =  this.updatedTime - this.startTime;
                }
                // var days = Math.floor(difference / (1000 * 60 * 60 * 24));
                var hours = Math.floor((this.difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                var minutes = Math.floor((this.difference % (1000 * 60 * 60)) / (1000 * 60));
                var seconds = Math.floor((this.difference % (1000 * 60)) / 1000);
                var milliseconds = Math.floor((this.difference % (1000 * 60)) / 100);
                hours = (hours < 10) ? "0" + hours : hours;
                minutes = (minutes < 10) ? "0" + minutes : minutes;
                seconds = (seconds < 10) ? "0" + seconds : seconds;
                milliseconds = (milliseconds < 100) ? (milliseconds < 10) ? "00" + milliseconds : "0" + milliseconds : milliseconds;
                document.querySelector('.timer').innerHTML = hours + ':' + minutes + ':' + seconds + ':' + milliseconds;
            },
            switchPages() {
                if(this.pageOne) {
                    // this.getScores();
                    alert(this.info[0]);
                    document.getElementById("page-one").hidden = true;
                    document.getElementById("page-two").hidden = false;
                    document.getElementById("slider-text").innerHTML = "Game";
                    this.pageOne = false;
                } else {
                    document.getElementById("page-one").hidden = false;
                    document.getElementById("page-two").hidden = true;
                    document.getElementById("slider-text").innerHTML = "Scores";
                    this.pageOne = true;
                }
            },
            addToJSONScores(choice) {
                if (choice == 0) {
                    this.scores[0].Score -= 1;
                } else if (choice == 1) {
                    this.scores[0].Score += 1;
                } else if (choice == 2) {
                    this.scores[1].Score -= 1;
                } else if (choice == 3) {
                    this.scores[1].Score += 1;
                }
                localStorage.setItem('scores', JSON.stringify(this.scores));

                var retrievedObject = localStorage.getItem('scores');
                console.log('retrievedScore: ', JSON.parse(retrievedObject));
            },
            // async getScores() {
            //     try {
            //         const response = await this.$http.get(
            //             "https://localhost:44376/api/scores"
            //         );
            //         // JSON responses are automatically parsed.
            //         this.info = response.data;
            //     } catch (error) {
            //         console.log(error);
            //     }
            // }
        }
    }
</script>

<style scoped>
th {
    width: 120px;
    color: white;
}
td, th {
    border: 2px solid black;
    padding: 8px;
}
tr:nth-child(even) {
    background-color: white;
    font-weight: bold;
}
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:ital,wght@1,300&display=swap');
    .wrapper {
  height: 5.5vh;
  /*This part is important for centering*/
  display: flex;
  /* align-items: center; */
  justify-content: center;
}

.typing-demo {
  width: 14ch;
  animation: typing 2s steps(22), blink .5s step-end infinite alternate;
  white-space: nowrap;
  overflow: hidden;
  border-right: 3px solid;
  font-family: monospace;
  font-size: 3em;
}

@keyframes typing {
  from {
    width: 0
  }
}
    
@keyframes blink {
  50% {
    border-color: transparent
  }
}

.button-container {
    margin-top: 5rem;
    display: flex;
    justify-content: center;
    background-color: white;
}

.button-container button {
    width: 200px;
    height: 60px;
    color: white;
    border: 2px solid black;
    background-color: rgba(9, 71, 241, 0.7);
}

.button-container button:hover {
    background-color: black;
}

#Monday {
    display: inline-block;
    color: white;
    background-color: black;
    width: 500px;
    height: 200px;
    margin-top: 5rem;
    font-family: 'Roboto Mono', monospace;
}

#Monday p {
    margin-top: 30px;
}

#Tuesday {
    display: inline-block;
    color: white;
    background-color: black;
    width: 500px;
    height: 200px;
    margin-top: 5rem;
    font-family: 'Roboto Mono', monospace;
}

#Tuesday p {
    margin-top: 30px;
}

#Wednesday {
    display: inline-block;
    color: white;
    background-color: black;
    width: 500px;
    height: 200px;
    margin-top: 5rem;
    font-family: 'Roboto Mono', monospace;
}

#Wednesday p {
    margin-top: 30px;
}

#Thursday {
    display: inline-block;
    color: white;
    background-color: black;
    width: 500px;
    height: 200px;
    margin-top: 5rem;
    font-family: 'Roboto Mono', monospace;
}

#Thursday p {
    margin-top: 30px;
}

#Friday {
    display: inline-block;
    color: white;
    background-color: black;
    width: 500px;
    height: 200px;
    margin-top: 5rem;
    font-family: 'Roboto Mono', monospace;
}

#Friday p {
    margin-top: 30px;
}

.outside-container {
    background-color: rgb(252, 3, 78);
    height: 800px;
    width: 600px;
    display: inline-block;
    border: 3px solid black;
    padding: 20px 20px 20px 20px;
    animation-duration: 1.5s;
    animation-name: zoomin;
}

@keyframes zoomin {
    from {
        width: 0;
        height: 0;
    }

    to {
        height: 800px;
        width: 600px;
    }
}

#safeTimer {
    margin-top: 50px;
    margin-bottom: -80px;
    background-color: rgb(255, 255, 255);
    width: 200px;
    display: inline-block;
}

#timerContainer {
  font-family: 'Source Sans Pro', sans-serif;
  font-weight: 300;
  width:600px;
  margin:20px auto;
  min-height: 60px;
  border-top:0px;
  display: inline-block;
}
.timer, .reset {
  float:left;
  width: 54%;
  padding: 20px 0;
  font-size: 24px;
  text-align:center;
  color: #fff;
  background: #A90000;
  cursor: pointer
}
.reset {
  background: #550000;
  color: white;
  width:14.9%;
  border-left: 1px solid #990000;
}
.reset:hover {
  background: #CC0000;
}
.lighter {
  background: #CC0000
}

#switch-container {
    width: 60px;
}

.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>