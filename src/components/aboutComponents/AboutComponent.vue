<script>
import $ from 'jquery'
$(document).ready(function () {
  const front = document.getElementsByClassName('front')
  const back = document.getElementsByClassName('back')
  console.log(front)
  console.log(back)
  let highest = 0
  let absoluteSide = ''

  for (let i = 0; i < front.length; i++) {
    if (front[i].offsetHeight > back[i].offsetHeight) {
      if (front[i].offsetHeight > highest) {
        highest = front[i].offsetHeight
        absoluteSide = '.front'
      }
    } else if (back[i].offsetHeight > highest) {
      highest = back[i].offsetHeight
      absoluteSide = '.back'
    }
  }
  $('.front').css('height', highest)
  $('.back').css('height', highest)
  $(absoluteSide).css('position', 'absolute')

})
</script>

<template>
  <div class="col aboutContainer">
    <h1 id="kniffel"><br>Kniffel - Game Rules</h1>
    <h2 id="game-summary">Game Summary</h2>
    <p>On each turn, roll the dice up to 3 times to get the highest scoring combination for one of 13 categories.
      After you finish rolling, you must place a score or a zero in one of the 13 category boxes on your score column.
      The game ends when all players have filled in their 13 boxes.
      Scores are totaled, including any bonus points. The player with the highest total wins.</p>
    <h2 id="taking-a-turn">Taking a turn</h2>
    <p>On your turn, you may roll the dice up to 3 times, although you may stop and score after your first or second roll.
      To roll the dice, click the dice Button.<br>
      <img src="src/assets/images/about_dice_button.png"/>
    </p>
    <h3 id="keep-dice-aside">Keep dice aside</h3>
    <p>After each roll you may want to set any &quot;keepers&quot; aside.
      To do so you can select the dice you want to keep by clicking on them.<br>
      <img src="src/assets/images/about_dice_right.png"/>
    </p>
    <h3 id="put-dice-back-into-the-cup">Put dice back into the cup</h3>
    <p>You may change your mind after any roll.
      At any time you can decide if you want to put dice back into the Cup.
      To do so you can click on the dice from the right-hand side just like you did before where you put
      them aside. You may also want to put all dice back in. Therefore, you can use the double left arrow button.</p><br>
      <img src="src/assets/images/about_dice_double_left.png"/>
    <h2 id="scoring">Scoring</h2>
    <p>When you are finished rolling, decide which box to fill in on your score column.
      You must fill in a box on each turn; if you can&#39;t (or don&#39;t want to) enter a score, you must enter a zero.
      To enter any score to your column you have to select one option on the left hand side of the GUI.</p><br><br>
      <img src="src/assets/images/about_field.png"/>
    <p>If you decide to click the &#39;Chance&#39;-Button then this Button will be disabled in your next round.</p>
    <h3 id="scoring-combinations">Scoring Combinations</h3>
    <p>To score in the Upper Section, only dice with the same number will count.<br><br>
      Your goal in the Upper Section is to score a total of at least 63 points, to earn a 35-point bonus.
      The bonus points are based on scoring of each number;
      however, you may earn the bonus with any combination of scores totaling 63 points or more.
      Each of the Lower Section scoring combinations is explained in detail in the next second column of the GUI.</p>
    <div class="container">
      <div style="width: 100%" class="row text-center">
        <div class="col-md-4 card-container">
          <div class="card card-flip">
            <div class="front card-block">
              <h4 class="card-title">3 of a Kind</h4>
              <p class="card-text">Score in this box only if the dice include 3 or more of the same number.</p>
            </div>
            <div class="back card-block">
              <h4 class="card-title">Scoring Combinations</h4>
              <div class="card-body" style="padding: 5% 2%">
                <div style="display: flex; height: 50px">
                  <div style="border: 2px solid red; border-radius: 10px; width: max-content;">
                    <img src="src/assets/images/6.png" alt=""/>
                    <img src="src/assets/images/6.png" alt=""/>
                    <img src="src/assets/images/6.png" alt=""/>
                  </div>
                  <img style="margin-left: 4.5px; margin-top: 2px" src="src/assets/images/5.png" alt=""/>
                  <img style="margin-left: 6px; margin-top: 2px" src="src/assets/images/4.png" alt=""/>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-4 card-container">
          <div class="card card-flip">
            <div class="front card-block">
              <h4 class="card-title">4 of a Kind</h4>
              <p class="card-text">Score in this box only if the dice include 4 or more of the same number.</p>
            </div>
            <div class="back card-block">
              <h4 class="card-title">Scoring Combinations</h4>
              <div class="card-body" style="padding: 5% 2%">
                <div style="display: flex; height: 50px">
                  <div style="border: 2px solid red; border-radius: 10px; width: max-content;">
                    <img src="src/assets/images/6.png" alt=""/>
                    <img src="src/assets/images/6.png" alt=""/>
                    <img src="src/assets/images/6.png" alt=""/>
                    <img src="src/assets/images/6.png" alt=""/>
                  </div>
                  <img style="margin-left: 4.5px; margin-top: 2px" src="src/assets/images/5.png" alt=""/>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-4 card-container">
          <div class="card card-flip">
            <div class="front card-block">
              <h4 class="card-title">Full House</h4>
              <p class="card-text">Score in this box only if the dice show three of one number and two of another. Any Full House is worth 25 points.</p>
            </div>
            <div class="back card-block">
              <h4 class="card-title">Scoring Combinations</h4>
              <div class="card-body" style="padding: 5% 2%">
                <img style="margin-top: 2px" src="src/assets/images/6.png" alt=""/>
                <img style="margin-top: 2px" src="src/assets/images/6.png" alt=""/>
                <img style="margin-top: 2px" src="src/assets/images/5.png" alt=""/>
                <img style="margin-top: 2px" src="src/assets/images/5.png" alt=""/>
                <img style="margin-top: 2px" src="src/assets/images/5.png" alt=""/>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-4 card-container">
          <div class="card card-flip">
            <div class="front card-block">
              <h4 class="card-title">Small Straight</h4>
              <p class="card-text">Score in this box only if the dice show any sequence of four numbers. Any Small Straight is worth 30 points.</p>
            </div>
            <div class="back card-block">
              <h4 class="card-title">Scoring Combinations</h4>
              <div class="card-body" style="padding: 5% 2%">
                <div style="display: flex; height: 50px">
                  <div style="border: 2px solid red; border-radius: 10px; width: max-content;">
                    <img src="src/assets/images/1.png" alt=""/>
                    <img src="src/assets/images/2.png" alt=""/>
                    <img src="src/assets/images/3.png" alt=""/>
                    <img src="src/assets/images/4.png" alt=""/>
                  </div>
                  <img style="margin-left: 4.5px; margin-top: 2px" src="src/assets/images/1.png" alt=""/>
                </div>
                <div style="display: flex; height: 50px; margin-top: 2px">
                  <div style="border: 2px solid red; border-radius: 10px; width: max-content;">
                    <img src="src/assets/images/2.png" alt=""/>
                    <img src="src/assets/images/3.png" alt=""/>
                    <img src="src/assets/images/4.png" alt=""/>
                    <img src="src/assets/images/5.png" alt=""/>
                  </div>
                  <img style="margin-left: 4.5px; margin-top: 2px" src="src/assets/images/4.png" alt=""/>
                </div>
                <div style="display: flex; height: 50px; margin-top: 2px">
                  <div style="border: 2px solid red; border-radius: 10px; width: max-content;">
                    <img src="src/assets/images/3.png" alt=""/>
                    <img src="src/assets/images/4.png" alt=""/>
                    <img src="src/assets/images/5.png" alt=""/>
                    <img src="src/assets/images/6.png" alt=""/>
                  </div>
                  <img style="margin-left: 4.5px; margin-top: 2px" src="src/assets/images/3.png" alt=""/>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-4 card-container">
          <div class="card card-flip">
            <div class="front card-block">
              <h4 class="card-title">Large Straight</h4>
              <p class="card-text">Score in this box only if the dice show any sequence of four numbers. Any Large Straight is worth 40 points.</p>
            </div>
            <div class="back card-block">
              <h4 class="card-title">Scoring Combinations</h4>
              <div class="card-body" style="padding: 5% 2%">
                <div style="display: flex; height: 50px; margin-top: 2px">
                  <div style="width: max-content;">
                    <img src="src/assets/images/1.png" alt=""/>
                    <img src="src/assets/images/2.png" alt=""/>
                    <img src="src/assets/images/3.png" alt=""/>
                    <img src="src/assets/images/4.png" alt=""/>
                    <img src="src/assets/images/5.png" alt=""/>
                  </div>
                </div>
                <div style="display: flex; height: 50px; margin-top: 2px">
                  <div style="width: max-content;">
                    <img src="src/assets/images/2.png" alt=""/>
                    <img src="src/assets/images/3.png" alt=""/>
                    <img src="src/assets/images/4.png" alt=""/>
                    <img src="src/assets/images/5.png" alt=""/>
                    <img src="src/assets/images/6.png" alt=""/>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-4 card-container">
          <div class="card card-flip">
            <div class="front card-block">
              <h4 class="card-title">Kniffel</h4>
              <p class="card-text">Score in this box only if the dice show five of the same number (5 of a kind). You can score 50 points in the Kniffel box.</p>
            </div>
            <div class="back card-block">
              <h4 class="card-title">Scoring Combinations</h4>
              <div class="card-body" style="padding: 5% 2%">
                <img style="margin-top: 2px" src="src/assets/images/2.png" alt=""/>
                <img style="margin-top: 2px" src="src/assets/images/2.png" alt=""/>
                <img style="margin-top: 2px" src="src/assets/images/2.png" alt=""/>
                <img style="margin-top: 2px" src="src/assets/images/2.png" alt=""/>
                <img style="margin-top: 2px" src="src/assets/images/2.png" alt=""/>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <h4 id="chance">Chance</h4>
    <p>Score the total of any 5 dice in this box. This catch-all category comes handy when you can&#39;t (or don&#39;t want
      to) score in another category, and don&#39;t want to enter a zero.<br><br>
    </p>
    <h3 id="ending-a-game">Ending a Game</h3>
    <p>Once each player has filled in all 13 category boxes, the game ends.</p>
    <h3 id="how-to-win">How to Win</h3>
    <p>After the scores are tallied, the player with the highest &#39;Endsumme&#39; wins the game!</p>
    <h2 id="save-a-game">Save a game</h2>
    <p>If you decide to continue playing your game of &#39;Kniffel&#39; later you are also able to save the current status
      of the game.
      To do so you can select 'Action' -> 'Save'.<br>
    </p>

    <h2 id="load-a-game">Load a game</h2>
    <p>When you want to load your saved game and continue where you left off you can load the saved game by selecting
      'Action' -> 'Load'
      <br><br>
    </p>
  </div>
</template>

<style scoped>
@import 'bootstrap/dist/css/bootstrap.min.css';

h1 {
  margin-top: 1%;
}

img {
  max-width: 100%;
}

body {
  background-image: radial-gradient(forestgreen, black 140%);
}

.aboutContainer {
  position: relative;
  font-size: larger;
  margin-top: -0.5%;
  margin-left: 25%;
  margin-right: 25%;
  color: white;
}

@media screen and (max-width: 600px) {
  .aboutContainer {
    margin-left: 10.5%;
    margin-right: 10.5%;
  }
}

@media screen and (max-width: 350px) {
  .aboutContainer {
    margin-left: 5%;
    margin-right: 5%;
  }
}

.card-block .btn-outline-primary {
  width: 100%;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
  bottom: 0;
  left: 0;
  position: absolute;
}

.card {
  margin: 20px 0;
}

/* Flip Cards CSS */
.card-container {
  min-width: 280px !important;
  perspective: 700px;
}
.card-flip {
  position: relative;
  align-items: center;
  min-width: 270px;
  width: 100%;
  transform-style: preserve-3d;
  height: auto;
  transition: all 0.5s ease-out;
  background-image: linear-gradient(to bottom, #9f4045, #9f4045 20%, lightgrey 15%);
  border: 2px solid black;
  border-radius: 15px;
}

.card-flip div {
  backface-visibility: hidden;
  transform-style: preserve-3d;
  height: 100%;
  border: none;
}

.card-flip .front {
  position: relative;
  width: 95%;
  z-index: 1;
}

.card-flip .back {
  position: relative;
  z-index: 0;
  transform: rotateY(-180deg);
  width: 100%;
}

.card-container:hover .card-flip {
  transform: rotateY(180deg);
}

.front.card-block {
  display: flex;
  flex-direction: column;
  padding-top: 15px;
  /*justify-content: center;*/
}

.back.card-block {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-top: 15px;
  align-items: center;
}

p.card-text {
  text-align: left;
  color: black;
}

h4.card-title {
  color: white;
}

.card-body img {
  max-height: 45px;
}
</style>
