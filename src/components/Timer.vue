<script setup>
import { ref, computed, onMounted } from "vue";

//現在の日時を処理
const date = ref(new Date());
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
}

.date {
  font-size: 20px;
  justify-content: right;
  padding-left: 40%;
}

.time {
  font-size: 80px;
}

.seconds {
  font-size: 40px;
}
</style>
