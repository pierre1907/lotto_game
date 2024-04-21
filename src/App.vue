Copy code
<template>
  <div class="lotto-container">
    <Lotto-header></Lotto-header>
    <div class="title">Numéros gagnants</div>
    <div class="result-container" id="resultat">
      <lotto-ball v-for="ball in winBalls" v-bind:number="ball" :key="ball"></lotto-ball>
    </div>
    <div class="bonus" v-if="bonus">Numéro bonus : <lotto-ball :number="bonus"></lotto-ball></div>

    <div class="button-container">
      <button v-if="redo" @click="onClickRedo" class="btn">Rejouer !</button>
    </div>

    <Lotto-footer></Lotto-footer>
  </div>
</template>

<script>
function getWinNumbers() {
  console.log('getWinNumbers');
  const candidate = Array(45).fill().map((v,i) => i+1);
  const shuffle = [];
  while(candidate.length > 0) {
    shuffle.push(candidate.splice(Math.floor(Math.random() * candidate.length),1)[0]);
  }
  const bonusNumber = shuffle[shuffle.length-1];
  const winNumbers = shuffle.slice(0, 6).sort((p,c) => p-c);
  return [...winNumbers, bonusNumber];
}

import LottoHeader from './components/LottoHeader.vue'
import LottoBall from './components/LottoBall.vue'
import LottoFooter from './components/LottoFooter.vue'


const timeouts=[];
export default {
  name: 'App',
  components: {
    LottoBall, // lotto-ball : LottoBall
    LottoHeader,
    LottoFooter,
  },
  data(){
    return{
      winNumbers : getWinNumbers(),
      winBalls:[],
      bonus:null,
      redo:false,
    }
  },
  computed:{

  },
  methods:{
    onClickRedo() {
       this.winNumbers = getWinNumbers();
      this.winBalls = [];
      this.bonus = null;
      this.redo = false;
       this.showBalls();
    },
    showBalls() {
       for (let i =0; i< this.winNumbers.length - 1; i++) {
        timeouts[i] = setTimeout(() => {
          this.winBalls.push(this.winNumbers[i]);
        },(i + 1) * 1000);
      }
       timeouts[6] = setTimeout(() => {
        this.bonus = this.winNumbers[6];
        this.redo = true;
      }, 7000)
    },
  },
  mounted() {
    this.showBalls();
  },
  beforeUnmount() {
    timeouts.forEach((t) => {
      clearTimeout(t);
    });
  },
  watch:{

  },
}
</script>

<style scoped>
  .lotto-container {
    text-align: center;
    padding: 20px;
  }

  .logo {
    width: 100px;
    height: auto;
    margin-bottom: 20px;
  }

  .title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
  }

  .result-container {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }

  .bonus {
    font-size: 18px;
    margin-bottom: 20px;
  }

  .button-container {
    text-align: center; /* Centre le contenu horizontalement */
    margin-top: 20px; /* Ajoute un espace au-dessus du bouton */
  }

  .btn {
    padding: 10px 20px; /* Ajoute un espace autour du texte du bouton */
    background-color: #007bff; /* Couleur de fond du bouton */
    color: #fff; /* Couleur du texte du bouton */
    border: none; /* Supprime la bordure */
    border-radius: 5px; /* Ajoute des coins arrondis */
    cursor: pointer; /* Change le curseur au survol */
    font-size: 16px; /* Taille de la police */
    transition: background-color 0.3s; /* Animation de transition pour la couleur de fond */
  }

  .btn:hover {
    background-color: #0056b3; /* Couleur de fond du bouton au survol */
  }
</style>
