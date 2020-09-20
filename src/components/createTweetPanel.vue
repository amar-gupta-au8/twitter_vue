<template>
  <form
    class="create-tweet"
    @submit.prevent="createNewTweet"
    :class="{ __exceded: newTweetCharacterCount > 120 }"
  >
    <label for="newTweet"
      ><strong>New Tweet ({{ newTweetCharacterCount }}/120)</strong></label
    >
    <textarea id="newTweet" rows="4" v-model="state.newTweetContent" />
    <div class="create-tweet-pannel-submit">
      <div class="create-tweet-type">
        <label for="newTweetType"><strong>Type: </strong></label>
        <select id="newTweetType" v-model="state.selectedTweetType">
          <option
            :value="option.value"
            v-for="(option, index) in state.tweetType"
            :key="index"
            >{{ option.name }}</option
          >
        </select>
      </div>
      <button type="submit">Tweet!</button>
    </div>
  </form>
</template>

<script>
import { reactive, computed } from 'vue';
export default {
  name: 'createTweetPanel',
  setup(props, ctx) {
    const state = reactive({
      newTweetContent: '',
      selectedTweetType: 'instant',
      tweetType: [
        { value: 'instant', name: 'Publish Tweet' },
        { value: 'draft', name: 'Draft' },
      ],
      followers: 0,
    });
    const newTweetCharacterCount = computed(() => state.newTweetContent.length);
    const createNewTweet = () => {
      if (state.newTweetContent && state.selectedTweetType !== 'draft') {
        ctx.emit('add-tweet', state.newTweetContent);
        state.newTweetContent = '';
      }
    };
    return { state, newTweetCharacterCount, createNewTweet };
  },
};
</script>

<style lang="scss" scoped>
.create-tweet {
  margin-top: 20px;
  border-top: 1px solid #dfe3e8;
  padding: 20px 0;
  display: flex;
  flex-direction: column;

  &.__exceded {
    color: red;
    border: red;
  }
  textarea {
    border: 1px solid #dfe3e8;
    border-radius: 5px;
  }
  .create-tweet-pannel-submit {
    display: flex;
    justify-content: space-between;
  }
  .create-tweet-type {
    padding: 10px 0;
  }
  button {
    padding: 5px 20px;
    margin: auto 0;
    border-radius: 5px;
    border: none;
    background: #00acee;
    color: #fff;
    font-weight: bold;
  }
}
</style>
