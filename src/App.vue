<template>
  <div id="app">
    <section class="row">
      <div class="small-6 columns">
        <h1 class="text-center">PLAYER</h1>
        <div class="wins">
          <div class="wins text-center" style="background-color: green; margin: 0; color: white;" v-bind:style="{width: userWidth}">
            {{userWins}}
          </div>
        </div>
      </div>
      <div class="small-6 columns">
        <h1 class="text-center">COMPUTER</h1>
        <div class="wins">
          <div class="wins text-center" style="background-color: green; margin: 0; color: white;" v-bind:style="{width: cpuWidth}">
            {{cpuWins}}
          </div>
        </div>
      </div>
    </section>
    <section class="row controls" v-show="isShown">
      <div class="small-12 columns">
        <button id="start-game" @click="isShown = !isShown">START NEW GAME</button>
      </div>
    </section>
    <section class="row controls" v-show="!isShown">
      <div class="small-12 columns">
        <button id="rock" @click="userRock">ROCK</button>
        <button id="paper" @click="userPaper">PAPER</button>
        <button id="scissors" @click="userScissors">SCISSORS</button>
        <button id="restart" @click= "restartGame">RESTART</button>
      </div>
    </section>
    <section class="row log" v-show="!isShown">
      <div class="small-12 columns">
        <ul v-bind:style="{backgroundColor: resultColor}">
          <li>
            {{results}}
          </li>
        </ul>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'app',
  data (){
    return {
      isShown: true,
      setRounds: 10,
      userWins: 0,
      cpuWins: 0,
      rounds: 0,
      results: '',
      resultColor: '',
      userWidth: '0%',
      cpuWidth: '0%'
    }
  },
  methods: {
//If the User picks Rock. Each choice will update rounds, wins, loses, and print results
    userRock: function(){

      let cc = Math.random(); //random choice selected for computer

      if (cc < 0.34) { //rock TIE
        this.rounds++;
        this.resultColor = 'hsl(240, 100%, 70%)';
        this.results = "Round: "+ this.rounds + ". You chose ROCK and the computer chose ROCK It's a tie.";
      } else if (cc > 0.34 && cc < 0.67) { //paper LOSE
        this.rounds++;
        this.cpuWins++;
        this.resultColor = 'hsl(0, 100%, 70%)';
        this.cpuWidth = (this.cpuWins * 10) + "%";
        this.results = "Round: "+ this.rounds + ". You chose ROCK and the computer chose PAPER. You lost...";
      } else { //scissors WIN
        this.userWins++;
        this.rounds++;
        this.resultColor = 'hsl(120, 100%, 70%)';
        this.userWidth = (this.userWins * 10) + "%";
        this.results = "Round: "+ this.rounds + ". You chose ROCK and the computer chose SCISSORS. You Won!";
      }
      //When 10 wins are present confirm box to play again appears. Resets data if OK selected
      if (this.userWins == 10){ //if the user wins
        if(confirm('You have won! Click OK to play again.')){
          this.rounds = 0;
          this.cpuWins = 0;
          this.userWins = 0;
          this.resultColor = 'yellow';
          this.results = "You have restarted, make choice to start again";
          this.cpuWidth = '0%';
          this.userWidth = '0%';
        } else{
          this.resultColor = 'black';
        }
      }
      else if (this.cpuWins ==10){ //if the computer wins
        if(confirm('You have won! Click OK to play again.')){
          this.rounds = 0;
          this.cpuWins = 0;
          this.userWins = 0;
          this.resultColor = 'yellow';
          this.results = "You have restarted, make choice to start again";
          this.cpuWidth = '0%';
          this.userWidth = '0%';
        } else{
          this.resultColor = 'black';
        }
      }
    },
//If the User picks Paper. Each choice will update rounds, wins, loses, and print results
    userPaper: function(){

      let cc = Math.random(); //random choice selected for computer

      if (cc < 0.34) { //rock WIN
        this.userWins++;
        this.rounds++;
        this.resultColor = 'hsl(120, 100%, 70%)';
        this.userWidth = (this.userWins * 10) + "%";
        this.results = "Round: "+ this.rounds + ". You chose PAPER and the computer chose ROCK. You Won!";
      } else if (cc > 0.34 && cc < 0.67) { //paper TIE
        this.rounds++;
        this.resultColor = 'hsl(240, 100%, 70%)'
        this.results = "Round: "+ this.rounds + ". You chose PAPER and the computer chose PAPER. It's a tie.";
      } else { //scissors LOSE
        this.rounds++;
        this.cpuWins++;
        this.resultColor = 'hsl(0, 100%, 70%)';
        this.cpuWidth = (this.cpuWins * 10) + "%";
        this.results = "Round: "+ this.rounds + ". You chose PAPER and the computer chose SCISSORS. You lost...";
      }
      //When 10 wins are present confirm box to play again appears. Resets data if OK selected
      if (this.userWins == 10){ //if the user wins
        if(confirm('You have won! Click OK to play again.')){
          this.rounds = 0;
          this.cpuWins = 0;
          this.userWins = 0;
          this.resultColor = 'yellow';
          this.results = "You have restarted, make choice to start again";
          this.cpuWidth = '0%';
          this.userWidth = '0%';
        } else{
          this.resultColor = 'black';
        }
      }
      else if (this.cpuWins ==10){ //if the computer wins
        if(confirm('You have won! Click OK to play again.')){
          this.rounds = 0;
          this.cpuWins = 0;
          this.userWins = 0;
          this.resultColor = 'yellow';
          this.results = "You have restarted, make choice to start again";
          this.cpuWidth = '0%';
          this.userWidth = '0%';
        } else{
          this.resultColor = 'black';
        }
      }
    },
//If the User picks Scissors. Each choice will update rounds, wins, loses, and print results
    userScissors: function(){

      let cc = Math.random(); //random choice selected for computer

      if (cc < 0.34) { //rock LOSE
        this.rounds++;
        this.cpuWins++;
        this.resultColor = 'hsl(0, 100%, 70%)';
        this.cpuWidth = (this.cpuWins * 10) + "%";
        this.results = "Round: "+ this.rounds + ". You chose SCISSORS and the computer chose ROCK, You lost...";
      } else if (cc > 0.34 && cc < 0.67) { //paper WIN
        this.rounds++;
        this.userWins++;
        this.resultColor = 'hsl(120, 100%, 70%)';
        this.userWidth = (this.userWins * 10) + "%";
        this.results = "Round: "+ this.rounds + ". You chose SCISSORS and the computer chose PAPER. You Won!";
      } else { //scissors TIE
        this.rounds++;
        this.resultColor = 'hsl(240, 100%, 70%)';
        this.results = "Round: "+ this.rounds + ". You chose SCISSORS and the computer chose SCISSORS. It's a tie.";
      }
      //When 10 wins are present confirm box to play again appears. Resets data if OK selected
      if (this.userWins == 10){ //if the user wins
        if(confirm('You have won! Click OK to play again.')){
          this.rounds = 0;
          this.cpuWins = 0;
          this.userWins = 0;
          this.resultColor = 'yellow';
          this.results = "You have restarted, make choice to start again";
          this.cpuWidth = '0%';
          this.userWidth = '0%';
        } else{
          this.resultColor = 'black';
        }
      }
      else if (this.cpuWins ==10){ //if the computer wins
        if(confirm('You have won! Click OK to play again.')){
          this.rounds = 0;
          this.cpuWins = 0;
          this.userWins = 0;
          this.resultColor = 'yellow';
          this.results = "You have restarted, make choice to start again";
          this.cpuWidth = '0%';
          this.userWidth = '0%';
        } else{
          this.resultColor = 'black';
        }
      }
    },
//Game and data is restarted when user clicks restart button
    restartGame: function(){
      this.rounds = 0;
      this.cpuWins = 0;
      this.userWins = 0;
      this.resultColor = 'yellow';
      this.results = "You have restarted, make choice to start again";
      this.cpuWidth = '0%';
      this.userWidth = '0%';
    }
  }
}
</script>

<style>
  .text-center {
    text-align: center;
  }

  .wins {
    width: 80%;
    color: black;
    height: 40px;
    background-color: #eee;
    margin: auto;
    transition: width 1000ms;
  }

  .controls, .log {
    margin-top: 30px;
    text-align: center;
    padding: 10px;
    border: 1px solid #ccc;
    box-shadow: 0px 3px 6px #ccc;
  }

  .turn {
    margin-top: 20px;
    margin-bottom: 20px;
    font-weight: bold;
    font-size: 22px;
  }

  .log ul {
    list-style: none;
    font-weight: bold;
    text-transform: uppercase;
  }

  .log ul li {
    margin: 5px;
  }

  .log ul .player-turn {
    color: green;
    background-color: #aaffb0;
  }

  .log ul .computer-turn {
    color: red;
    background-color: #ffc0c1;
  }

  .log ul .tie-turn {
    color: blue;
    background-color: #e4e8ff;
  }

  button {
    font-size: 20px;
    background-color: #eee;
    padding: 12px;
    box-shadow: 0 1px 1px black;
    margin: 10px;
  }

  #start-game {
    background-color: #e4e8ff;
  }

  #start-game:hover {
    background-color: #687eff;
  }

  #rock {
    background-color: #ff7367;
  }

  #rock:hover {
    background-color: #ff3f43;
  }

  #paper {
    background-color: #ffaf4f;
  }

  #paper:hover {
    background-color: #ff9a2b;
  }

  #scissors {
    background-color: #aaffb0;
  }

  #scissors:hover {
    background-color: #76ff7e;
  }

  #restart {
    background-color: #ffffff;
  }

  #restart:hover {
    background-color: #c7c7c7;
  }
</style>
