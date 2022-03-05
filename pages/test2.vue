<template>
  <div
    class="
      container
      w-full
      mx-auto
      p-0
      m-0
      bg-white
      rounded
      border-orange-50
      text-black
      shadow-md
    "
  >
    <div class="flex justify-end">
      <input
        type="number"
        placeholder="Điểm"
        class="p-2 px-4 mt-4 rounded-md"
      />
      <select class="mx-4 mt-4 p-2 rounded-md">
        <option>Câu 1</option>
        <option>Câu 2</option>
        <option>Câu 3</option>
        <option>Câu 4</option>
      </select>
    </div>
    <div class="flex justify-center mt-6 ml-4">
      <textarea
        v-model="cword.question"
        class="
          resize-none
          rounded-md
          shadow-md
          focus:border-blue-400 focus:bg-white
          hover:focus:border-blue-400
        "
        cols="96"
        rows="4"
        placeholder="Nội dung câu hỏi "
      ></textarea>
      <textarea
        v-model="cword.answer"
        class="
          resize-none
          rounded-md
          shadow-md
          focus:border-blue-400 focus:bg-white
          hover:focus:border-blue-400
        "
        cols="96"
        rows="4"
        placeholder="Nội dung đáp án"
      ></textarea>
    </div>
    <div class="flex justify-center mt-6 ml-4 space-x-16">
      <div class="w-1/2 text-center">
        <div v-for="item in res" :key="item.question" class="min-w-max">
          <!-- <el-input type="text" v-model="item.question">{{item}} </el-input> -->
          {{ item }}
        </div>
      </div>
      <div class="w-1/2 text-center">
        <div v-for="item in res" :key="item.answer">
          <button
            type="button"
            class="
              rounded-md
              mb-4
              py-4
              px-4
              bg-gray-300
              hover:text-blue-400 hover:bg-blue-100
              text-black
            "
          >
            {{ item.answer }}
          </button>
        </div>
      </div>
    </div>

    <div class="ml-4">
      <button
        type="button"
        class="
          bg-gray-300
          text-gray-900
          rounded
          hover:text-blue-400 hover:bg-blue-100
          px-4
          py-2
          mb-4
          focus:outline-none
        "
        @click="OnSubmit"
      >
        add answer
      </button>
    </div>
    <div class="flex justify-center mb-4">
      <button
        type="button"
        class="
          bg-gray-300
          text-gray-900
          rounded
          hover:text-blue-400 hover:bg-blue-100
          px-4
          py-2
          mb-4
          focus:outline-none
        "
        @click="OnSubmit"
      >
        Save
      </button>
    </div>
    <div>
      <button
        type="button"
        class="bg-red-600 p-3 rounded text-white"
        @click="OnDelete"
      >
        Delete
      </button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data() {
    return {
      res: [],
      cword: {
        answer: '',
        question: '',
      },
    }
  },
  created() {
    this.getdata()
  },
  methods: {
    getdata() {
      axios
        .get('https://6214967f89fad53b1f17fd73.mockapi.io/api/noitu/Admin')
        .then((res) => {
          this.res = res.data
        })
    },
    OnSubmit() {
      axios({
        method: 'post',
        url: 'https://6214967f89fad53b1f17fd73.mockapi.io/api/noitu/Admin',
        data: {
          question: this.cword.question,
          answer: this.cword.answer,
        },
      }).then((res) => {
        this.getdata()
      })
    },
    OnDelete() {
      axios({
        method: 'delete',
        url: 'https://6214967f89fad53b1f17fd73.mockapi.io/api/noitu/Admin',
        data() {},
      })
    },
  },
}
</script>
