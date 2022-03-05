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
      <el-input placeholder="điền câu hỏi" class="align-middle">
        đáp án
      </el-input>
    </div>
    <div class="flex justify-center mt-6 ml-4 space-x-16">
      <div>
        <div v-for="(q, index) in questions" :key="q">
          Câu hỏi {{ index }}
          <el-input
            v-model="q.question.content"
            placeholder="Please input"
          ></el-input>
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
        url: 'http://127.0.0.1:4000/api/books',
        data() {},
      })
    },
  },
}
</script>
