<template>
    <div>
        <h1 id="title">Rock Paper Scissors</h1>
        <h2>Your Score: {{playerGained}}</h2>
        <h2>Computer's Score: {{computersGained}}</h2>
        <div id="buttons">
            <button class="button-os" @click="rock">Rock</button>
            <button class="button-os" @click="paper">Paper</button>
            <button class="button-os" @click="scissors">Scissors</button>
            <button class="button-os" @click="reset">Reset Scores</button>
        </div>
        
        <h1 id="result">{{resultGame}}</h1>
    </div>
</template>

<script>
export default {
    data(){
        return{
            computersPlay: '',
            usersPlay: '',
            resultGame: '',
            computersGained: 0,
            playerGained: 0,
        }
    },

    methods:{
        computerPlay(){
            let play = ['Rock', 'Paper','Scissors'];
            let index = Math.floor(Math.random()*play.length);
            this.computersPlay= play[index];
        },

        playRound(playerSelection, computerSelection) {
            console.log(`Computer selected ${computerSelection}`);
            let player = playerSelection.toLowerCase();
            let computer = computerSelection.toLowerCase();
            let equal =  player === computer ? true: false;
            if (equal) {this.resultGame = `Try again.  You both selected ${playerSelection}`}
            else if (player === 'paper') {
                computer === 'rock' ? 
                this.calculateStatistics('You win.  Paper covers Rock',0): 
                this.calculateStatistics('You lose. Scissors cuts Paper',1);
            }else if (player === 'rock') {
                computer === 'scissors'?
                this.calculateStatistics('You won. Rock “crushes” scissors',0):
                this.calculateStatistics('You lose. Paper covers Rock',1);
            }else{
                computer === 'rock'?
                this.calculateStatistics('You lose. Scissors is “crushed” by rock',0):
                this.calculateStatistics('You won. Scissors “cuts” paper',1);
            }
                
        },

        rock(){
            this.usersPlay = 'Rock',
            console.log(this.usersPlay);
            this.game();
        },

        paper(){
            this.usersPlay = 'Paper',
            console.log(this.usersPlay);
            this.game();
        },

        scissors(){
            this.usersPlay = 'Scissors',
            console.log(this.usersPlay);
            this.game();
        },

        reset(){
            this.playerGained = 0;
            this.computersGained=0;
        },

        calculateStatistics(message,who){
            this.resultGame = message;
            who === 0 ? this.playerGained++:this.computersGained++;
        },

        game(){
            this.computerPlay();
            this.playRound(this.usersPlay, this.computersPlay);
            console.log(this.resultGame);
        }
    }
}
</script>

<style scoped>
    
    #buttons{
        display: inline-flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-evenly;
        align-items: flex-start;
    }
    button{
        border: solid 1px greenyellow;
        border-radius: 15px;
        box-shadow: 0 0 8px rgb(207, 207, 207);
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        font-size: large;
        padding: 3%;
        margin: 3%;
    }
   
   
  
</style>