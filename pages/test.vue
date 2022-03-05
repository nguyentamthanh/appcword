<template>
  <div
    class="
      container
      w-full
      mx-auto
      p-0
      m-0
      bg-gray-500
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
    <br />
    <el-input
      v-model="questions.question.content"
      type="textarea"
      :rows="2"
      :column="2"
      placeholder="Điền câu hỏi"
    ></el-input>

    <div class="w-full flex mt-6 justify-center space-x-20">
      <div class="w-1/2 text-center">
        <div v-for="a in list1" :key="a" class="mt-4">
          <el-input v-model="a.content" type="textarea" :rows="2"></el-input>
        </div>
      </div>
      <div class="w-1/2 text-center">
        <div v-for="a in list2" :key="a" class="mt-4">
          <el-input v-model="a.content" type="textarea" :rows="2"></el-input>
        </div>
      </div>
    </div>
    <br />
    <el-button type="danger" plain @click="AddQuestion">Add Answer</el-button>
    <el-button type="danger" plain @click="Save">save</el-button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data() {
    return {
      list1: '',
      list2: '',
      questions: {
        question: {
          content: '',
        },
        answer: [
          {
            id: 1,
            group: 1,
            title: 'A',
            content: '',
          },
          {
            id: 2,
            group: 1,
            title: 'B',
            content: '',
          },
          {
            id: 3,
            group: 2,
            title: 'C',
            content: '',
          },
          {
            id: 4,
            group: 2,
            title: 'D',
            content: '',
          },
        ],
      },
    }
  },
  created() {
    // console.log(this.questions[0].answer.filter(x=>x.group===1))
    this.adddata()
  },
  methods: {
    AddQuestion() {
      this.questions.answer.push(
        {
          id: '',
          group: 1,

          title: 'A',
          content: '',
        },
        {
          id: '',
          group: 2,
          title: 'A',
          content: '',
        }
      )
      this.adddata()
    },
    adddata() {
      this.list1 = this.questions.answer.filter((x) => x.group === 1)
      this.list2 = this.questions.answer.filter((x) => x.group === 2)
    },

    Save() {
      axios({
        method: 'post',
        url: 'https://6214967f89fad53b1f17fd73.mockapi.io/api/noitu/q',
        data: {
          question: this.questions.question,
          answer: this.questions.answer,
        },
      }).then((res) => {
        this.$router.push('/data')
      })
    },
  },
}
</script>

<style scoped></style>
