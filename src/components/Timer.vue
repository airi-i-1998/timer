<script setup>
import { ref, computed, onMounted } from "vue";

//現在の日時を取得
const date = ref(new Date());
// データの変更に伴って自動的に再計算される
const year = computed(() => date.value.getFullYear());
const month = computed(() => date.value.getMonth() + 1);
const day = computed(() => dateTimePadding(date.value.getDate()));
const hours = computed(() => dateTimePadding(date.value.getHours()));
const minutes = computed(() => dateTimePadding(date.value.getMinutes()));
const seconds = computed(() => dateTimePadding(date.value.getSeconds()));

// /日時を2桁に変換
function dateTimePadding(num) {
  // numが一桁の場合にも必ず2桁の文字列を作り出すための手法
  return ("0" + num).slice(-2);
}

//現在の日時をセット
function setDate() {
  date.value = new Date();
}

// HTMLが読み込まれた際に実行される仕組み
onMounted(() => {
  // 現在の日時をセット
  setDate();
  // 1秒ごとにsetDate()を実行し、computed（）の関数が連動して実行されることで時間が表示される
  // setInterval：一定の間隔で指定された関数を繰り返し実行するためのJavaScriptのメソッド
  setInterval(() => {
    date.value = new Date();
  }, 1000);
});

// デフォルトを10秒で設定
const selectedTime = ref(10000);

function setAlarm() {
  window.setTimeout(() => {
    alert(`${selectedTime.value / 1000}秒経過しました！`);
  }, selectedTime.value);
}
</script>

<template>
  <div class="container">
    <div class="date">
      <p>{{ year }}/{{ month }}/{{ day }}</p>
    </div>
    <div>
      <p class="time">
        {{ hours }}：{{ minutes }}
        <span class="seconds">：{{ seconds }}</span>
      </p>
    </div>
    <div class="timer">
    <p class="set">
      <select v-model="selectedTime" class="set-time">
        <option value="10000">10秒</option>
        <option value="30000">30秒</option>
        <option value="60000">1分</option>
        <option value="300000">5分</option>
        <option value="600000">10分</option>
        <option value="1800000">30分</option>
        </select>
        後にアラーム
      </p>
      <span class="button" @click="setAlarm()">設定</span>
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 60%;
  height: 100%;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
  background-color: black;
  padding: 40px;
  margin: 25% 40px;
  border-radius: 10px;
}

p {
  margin: 0px;
}

.date,
.time {
  font-weight: 700;
  color: lawngreen;
  font-size: 80px;
}

.date {
  font-size: 20px;
  justify-content: right;
  padding-left: 40%;
}

.seconds {
  font-size: 40px;
}

.timer{
  display: flex;
}

.set {
  color: beige;
  margin: 5px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
}

.set-time {
  font-size: 20px;
  font-weight: 500;
  margin-right: 5px;
  border-radius: 8px;
  padding: 5px;
}

.button {
  border: 2px solid lawngreen;
  background-color: lawngreen;
  text-align: center;
  padding: 5px;
  margin: 5px;
  cursor: pointer;
  border-radius: 8px;
  font-size: 15px;
}

.button:hover {
  background-color: limegreen;
  border: 2px solid limegreen;
}
</style>
