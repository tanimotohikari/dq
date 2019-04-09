<template>
  <div class="contents">
    <audio id="js-sound-bgm" preload="auto" autoplay>
      <source src="sound/battle.mp3" type="audio/mp3" />
    </audio>
    <audio id="js-sound-end" preload="auto">
      <source src="sound/end.mp3" type="audio/mp3" />
    </audio>
    <audio id="js-sound-levelUp" preload="auto">
      <source src="sound/level-up.mp3" type="audio/mp3" />
    </audio>
    <div class="monsters">
      <ul class="monsters-list">
        <li v-for="(item, index) in monsterList" v-bind:key="item.id">
          {{ item.name }} HP：{{ item.hp }}
          <div class="monsters-list-inner">
            <img :src="item.src" :alt="item.name" />
          </div>
          <span v-if="item.hp === 0">死亡</span>
          <button v-if="item.hp !== 0" v-on:click="attackMonster(index)" class="l-bottom-small">攻撃する</button>
          <audio id="js-sound-attack" preload="auto">
            <source src="sound/se-attack.mp3" type="audio/mp3" />
          </audio>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      monstersHp: [false, false, false],
      monsterList: [
        { id: 1, name: 'スライム', hp: 10, src: '../icons/monster01.png' },
        { id: 2, name: 'オオムカデ', hp: 30, src: '../icons/monster02.png' },
        { id: 3, name: 'ミニドラゴン', hp: 40, src: '../icons/monster03.png' },
      ],
    };
  },
  methods: {
    /*
      モンスターを攻撃する
    */
    attackMonster: function(index) {
      this.monsterList[index].hp -= 10;
      document.getElementById('js-sound-attack').play();
      if (this.monsterList[index].hp === 0) {
        this.monstersHp[index] = true;
      }

      if (this.monstersHp[0] && this.monstersHp[1] && this.monstersHp[2]) {
        document.getElementById('js-sound-bgm').pause();

        var random = Math.floor(Math.random() * 11);
        if (random === 7) {
          document.getElementById('js-sound-levelUp').play();
        } else {
          document.getElementById('js-sound-end').play();
        }
      }
    },
  },
};
</script>
