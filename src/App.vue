<script setup lang="ts">

function logLevel (level: string) {
  console.log(level);
}
</script>

<template>
  <div class="wrapper">
    <div>
      Mouse enter block
      <div @mouseenter="() => logLevel('level 1')" class="enter">
        Level 1
        <div @mouseenter="() => logLevel('level 2')" class="enter">
          Level 2
        </div>
      </div>
    </div>
    <div>
      Mouse over block
      <div @mouseover="() => logLevel('level 1')" class="over">
        Level 1
        <div @mouseover="() => logLevel('level 2')" class="over">
          Level 2
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  gap: 5rem;
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
