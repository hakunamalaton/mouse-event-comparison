<script setup lang="ts">

function logLevel (level: string) {
  console.log(level);
}
</script>

<template>
  <div @mouseenter="() => logLevel('level 1')" class="enter">
    Level 1
    <div @mouseenter="() => logLevel('level 2')" class="enter">
      Level 2
      <div @mouseenter="() => logLevel('level 3')" class="enter">
        Level 3
        <div @mouseenter="() => logLevel('level 4')" class="enter">
          Level 4
        </div>
      </div>
    </div>
  </div>
  <div class="divider" />
  <div @mouseover="() => logLevel('level 1')" class="over">
    Level 1
    <div @mouseover="() => logLevel('level 2')" class="over">
      Level 2
      <div @mouseover="() => logLevel('level 3')" class="over">
        Level 3
        <div @mouseover="() => logLevel('level 4')" class="over">
          Level 4
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.divider {
  padding: 20px 0;
}
.enter, .over {
  padding: 30px;
  border: 1px solid red;
  margin: 10px;
}
</style>
