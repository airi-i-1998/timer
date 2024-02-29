<script setup>
import { ref, computed, onMounted } from 'vue';

//現在の日時を処理
const date = ref(new Date());
const year = computed(() => date.value.getFullYear());
const month = computed(() => date.value.getMonth() + 1);
const day = computed(() => dateTimePadding(date.value.getDate()));
const hours = computed(() => dateTimePadding(date.value.getHours()));
const minutes = computed(() => dateTimePadding(date.value.getMinutes()));
const seconds = computed(() => dateTimePadding(date.value.getSeconds()));

  // /日時を2桁に変換
  function dateTimePadding(num){
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
    date.value = new Date();}, 1000);
});
</script>

<template>
  <div>
    <div>
      <p>{{ year }}/{{ month }}/{{ day }}</p>
    </div>
    <div>
      <p>
        {{ hours }}:{{ minutes }}
        <span>
          :{{ seconds }}
        </span>
      </p>
    </div>
  </div>
</template>
