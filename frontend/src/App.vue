<script setup lang="ts">
import { syncedStore, getYjsDoc } from "@syncedstore/core";
import { WebrtcProvider } from "y-webrtc";
import { enableVueBindings } from "@syncedstore/core";
import * as Vue from "vue";

enableVueBindings(Vue);

type Something = { id: number };

const shape = {
  somethings: [] as Something[],
  someNumbers: {} as { a: number | undefined, b: number | undefined },
};

const store = syncedStore(shape);
const doc = getYjsDoc(store);

new WebrtcProvider("chose-a-room-id", doc, { signaling: ['ws://localhost:4444'] });

function addSomething() {
  store.somethings.push({ id: Math.random() * 100000 });
}

function increaseA () {
  if (store.someNumbers.a === undefined) {
    store.someNumbers.a = 1
    return
  }
  store.someNumbers.a += 1
}

function increaseB () {
  if (store.someNumbers.b === undefined) {
    store.someNumbers.b = 1
    return
  }
  store.someNumbers.b += 1
}

function removeSomething(id: number) {
  const index = store.somethings.findIndex(item => item.id === id);
  if (index !== -1) {
    store.somethings.splice(index, 1);
  }
}
</script>

<template>
  <div class="container">
    <div class="head">
      <div @click="addSomething" class="button">Add</div>
      <div @click="increaseA" class="button">Increase a</div>
      <div @click="increaseB" class="button">Increase b</div>
    </div>
    <div class="container-body">
      <div class="content">
        <div class="some-num">
          <span class="label">a</span>
          <span class="value">{{ store.someNumbers.a || 0 }}</span>
        </div>
        <div class="some-num">
          <span class="label">b</span>
          <span class="value">{{ store.someNumbers.b || 0 }}</span>
        </div>
      </div>
      <div class="content">
        <template v-for="something in store.somethings" :key="something.id">
          <div class="some">
            <div>{{ something.id }}</div>
            <div @click="removeSomething(something.id)" class="remove-button">Remove</div>
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
}
.head {
  margin-bottom: 1px;
}
.button, .some, .remove-button {
  padding: 4px;
  display: inline-block;
  cursor: pointer;
  border-radius: 4px;
  font-size: 12px;
  user-select: none;
}
.button {
  padding: 4px 8px;
  margin-right: 2px;
}
.some {
  padding: 4px 4px 4px 12px;
  margin-bottom: 2px;
}
.button {
  background: #2c3e50;
  color: white;
}
.some {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #b4b9bc;
  color: white;
  position: relative;
  margin: 1px;
}
.some-num {
  padding: 4px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #276791;
  color: white;
  position: relative;
  border-radius: 4px;
  margin: 1px;
}
.some-num span {
  font-size: 12px;
  padding: 4px;
  border-radius: 4px;
}
.some-num span.value {
  background: white;
  color: #2c3e50;
}
.remove-button {
  background: #b62d20;
  color: white;
  margin-left: 10px;
}
.container-body {
  display: flex;
}
.content {
  display: flex;
  flex-direction: column;
}
</style>
