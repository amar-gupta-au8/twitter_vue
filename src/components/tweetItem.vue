<template>
  <div class="tweet-item">
    <div class="user-profile_tweet">
      <div class="tweet-itew_user">@{{ userName }}</div>
      <div class="tweet-item_content">
        {{ tweet.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TweetItem',
  props: {
    userName: {
      type: String,
      required: true,
    },
    tweet: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
.tweet-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  &:hover {
    transform: scale(1.1, 1.1);
  }
  .tweet-item_user {
    font-weight: bold;
  }
}
</style>
