<template>
  <main>
  <h1>Polls to Vote On</h1>
  <section>
    <div class="polls-list"> 
      <!-- Poll Main Content -->
      <div v-if="this.error">Error loading Polls</div>
      <div v-else v-for="poll in polls">
        <router-link class="poll-link" :to="{name: 'poll', params: { id: poll._id }}">{{ poll.question }}</router-link>
    </div>
  </div>
  </section>
  </main>    
</template>

<script>
import Poll from './Poll.vue'

export default {
  data () {
    return {
      polls: [],
      error: null
    }
  },
  async created () {
    try {
      const response = await fetch('http://localhost:4040/polls', {
          'credentials': 'include'
        })
      if (response.ok) {
        this.polls = await response.json()
      } else {
        throw new Error('error')
      }
    } catch (err){
      this.error = err
    }
  },
  components: {
    Poll
  }
}
</script>

<style lang="scss" scoped>
@import '../style/vars';
h1 {
  text-align: center;
  color: $secondary-text-color-dark;
}
</style>
