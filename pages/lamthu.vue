<template>
  <div
    class="
      container
      w-full
      mx-auto
      p-0
      m-0
      bg-bg-white
      rounded
      border-orange-50
      text-black
      shadow-md
    "
  >
    <div v-for="(item, index) in test" :key="item">
      <div class=" text-center border-2 border-yellow-500 mx-8">Câu {{ index + 1 }}</div>
      <div class="w-full mt-6 flex space-x-20 justify-center">
        <div class="w-1/2 justify-center">
          <div v-for="i in item.list1" :key="i" class="w-90 mt-4 mx-auto">
            <el-button class="w-full" type="danger" plain>{{
              i.content
            }}</el-button>
          </div>

          <br />
        </div>
        <div class="w-1/2 text-center">
          <div v-for="i in item.list2" :key="i" class="w-90 mt-4 mx-auto">
            <el-button class="w-full" type="success" plain>{{
              i.content
            }}</el-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data() {
    return {
      list1: [],
      list2: [],
      test: {},
    }
  },
  created() {
    this.getdata()
  },
  methods: {
    getdata(id) {
      axios
        .get('https://6214967f89fad53b1f17fd73.mockapi.io/api/noitu/q')
        .then((res) => {
          // this.test = res?.data?.question
          // this.list1 = res?.data.answer.filter((x) => x.group === 1)
          // this.list2 = res?.data.answer.filter((x) => x.group === 2)
          this.test = res.data.map((i) => {
            i.list1 = i.answer.filter((x) => x.group === 1)
            i.list2 = i.answer.filter((x) => x.group === 2)
            return i
          })
        })
    },
  },
}
</script>

<style>
</style>
