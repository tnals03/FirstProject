<template>
  <v-main>
    <div align="center">
      <board-register-form @submit="onSubmit"/>
    </div>
  </v-main>
</template>

<script>
import BoardRegisterForm from '@/components/board/BoardRegisterForm'
import axios from 'axios'
export default {
  name: 'BoardRegisterPage',
  components: {
    BoardRegisterForm
  },
  methods: {
    onSubmit (payload) {
      console.log('BoardRegisterPage onSubmit()')
      const { title, writer, content } = payload
      axios.post('http://localhost:5555/boards', { title, writer, content })
        .then(res => {
          console.log(res)
          // 성공했다는 알림 띄움.
          alert('게시글 등록 성공!!')
          this.$router.push({
            name: 'BoardReadPage',
            params: { boardNo: res.data.boardNo.toString() }
          })
        })
        // 에러 발생했을 때 에러메세지 띄워줌
        .catch(err => {
          alert(err.response.data.message)
        })
    }
  }
}
</script>
