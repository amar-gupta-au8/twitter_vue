<template>
  <div class="user-profile">
    <div class="user-panel">
      <h1 class="username">@{{ state.user.userName }}</h1>
      <div class="admin-badge" v-if="state.user.isAdmin">Admin</div>
      <div class="admin-badge" v-else>User</div>
      <div class="follower-count">
        <strong>Followers: {{ state.followers }}</strong>
      </div>
      <CreateTweetPanel @add-tweet="addTweet" />
      <!-- thisone -->
    </div>
    <div class="tweets-wrapper">
      <TweetItem
        v-for="tweet in state.user.tweets"
        :key="tweet.id"
        :userName="state.user.userName"
        :tweet="tweet"
      />
    </div>
  </div>
</template>

<script>
import TweetItem from '../components/tweetItem';
import CreateTweetPanel from '../components/createTweetPanel';
import { computed, reactive } from 'vue';
import { useRoute } from 'vue-router';
import { users } from '../assets/user';
export default {
  name: 'userProfile',
  components: { TweetItem, CreateTweetPanel },
  setup() {
    const router = useRoute();
    const userId = computed(() => router.params.userId);

    const state = reactive({
      followers: 0,
      user: users[userId.value - 1] || users[0],
    });
    const addTweet = (tweet) => {
      state.user.tweets.unshift({
        id: state.user.tweets.length + 1,
        content: tweet,
      });
    };
    return { state, addTweet };
  },
};
</script>

<style scoped lang="scss">
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;
  .user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    margin-bottom: auto;
    .admin-badge {
      background: rebeccapurple;
      color: #fff;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
      margin-bottom: 20px;
    }
    h1 {
      margin: 0;
    }
  }
  .tweets-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}
</style>
