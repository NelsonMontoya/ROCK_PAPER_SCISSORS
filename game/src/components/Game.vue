<template>
    <div>
        <h1>Rock Paper Scissors</h1>
        <h1>{{resultGame}}</h1>
        <h2>Your Score: {{playerGained}}</h2>
        <h2>Computer's Score: {{computersGained}}</h2>
        <button @click="rock">Rock</button>
        <button @click="paper">Paper</button>
        <button @click="scissors">Scissors</button>
        <button @click="reset">Reset Scores</button>
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
    
</style>