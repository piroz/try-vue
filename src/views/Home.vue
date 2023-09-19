<template>
  <h1 class="text-3xl font-bold underline">Hello world!!</h1>
  <button
    class="shadow bg-red-500 hover:bg-red-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded"
    @click="state.count++">
    {{ state.count }}
  </button>
  <a :[attributeName]="url">About</a>
  <span @[eventName]="dosomething">{{ bar }}</span>
  <button @click="increment"
    class="shadow bg-red-500 hover:bg-red-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded">
    {{ count }}
  </button>
  <button @click="mutateDeeply"
    class="shadow bg-red-500 hover:bg-red-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded">
    {{ obj.nested.count }}</button>
  <div v-for="item in  obj.arr" class="bg-red-200 w-auto inline-block rounded-full py-2 px-4">{{ item }}</div>
  <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <div class="bg-orange-100 border-l-4 border-orange-500 text-orange-700 p-4" role="alert">
      <p class="font-bold">Be Warned</p>
      <p>Something not ideal might be happening.</p>
    </div>
    <div class="md:flex md:items-center mb-6">
      <div class="md:w-1/3">
        <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-full-name">
          Full Name
        </label>
      </div>
      <div class="md:w-2/3">
        <input
          class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500"
          id="inline-full-name" type="text" value="Jane Doe">
      </div>
    </div>
    <div class="md:flex md:items-center mb-6">
      <div class="md:w-1/3">
        <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-password">
          Password
        </label>
      </div>
      <div class="md:w-2/3">
        <input
          class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500"
          id="inline-password" type="password" placeholder="******************">
      </div>
    </div>
    <div class="md:flex md:items-center mb-6">
      <div class="md:w-1/3"></div>
      <label class="md:w-2/3 block text-gray-500 font-bold">
        <input class="mr-2 leading-tight" type="checkbox" @[eventName].prevent="whenChecked">
        <span class="text-sm">
          チェックボックス
        </span>
      </label>
    </div>
    <div class="md:flex md:items-center">
      <div class="md:w-1/3"></div>
      <div class="md:w-2/3">
        <button
          class="shadow bg-red-500 hover:bg-red-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded"
          type="button">
          Sign Up
        </button>
      </div>
    </div>
  </form>
</template>

<script setup>
import { nextTick, ref, reactive } from 'vue'

const state = reactive({ count: 0 })
const count = ref(0)


const increment = async () => {
  count.value++
  await nextTick()
  console.log(Date.now())
}
const bar = ref('href')
const url = ref('javascript:void(0)')
const attributeName = 'href'
const eventName = 'click'
const dosomething = () => {
  console.log('click')
}
const whenChecked = () => {
  console.log('checked')
}
const fog = 'title'

const obj = ref({
  nested: { count: 0 },
  arr: ['foo', 'bar']
})

function mutateDeeply() {
  // これらは期待通りに動作します。
  obj.value.nested.count++
  obj.value.arr.push('baz')

  if (obj.value.arr.length > 5) {
    obj.value.arr.splice(2)
  }
}

const raw = {}
const proxy = reactive(raw)
// プロキシはオリジナルと同じではありません。
console.log(proxy === raw) // false
// calling reactive() on the same object returns the same proxy
console.log(reactive(raw) === proxy) // true

// calling reactive() on a proxy returns itself
console.log(reactive(proxy) === proxy) // true

const proxy2 = reactive({})

const raw2 = {}
proxy2.nested = raw2

console.log(proxy2.nested === raw2) // false
</script>
