<template>
  <div class="bg-white rounded shadow w-2/3 p-4">
    <div class="flex justify-between items-center">
      <div>
        <div class="w-8">
          <img
            :src="authUser.data.attributes.profile_image.data.attributes.path"
            class="object-cover w-8 h-8 rounded-full"
          />
        </div>
      </div>
      <div class="flex-1 flex mx-4">
        <input
          v-model="postMessage"
          type="text"
          class="w-full pl-4 h-8 bg-gray-200 rounded-full bg-gray-200 focus:outline-none focus:shadow-outline text-sm"
          name="body"
          placeholder="Add a post"
        />
        <transition name="fade">
          <button
            v-if="postMessage"
            @click="$store.dispatch('postMessage')"
            class="bg-gray-200 ml-2 px-3 py-1 rounded-full"
          >Post</button>
        </transition>
      </div>
      <div>
        <button class="flex justify-center items-center w-10 h-10 rounded-full bg-gray-400">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="fill-current w-5 h-5">
            <path
              d="M21.8 4H2.2c-.2 0-.3.2-.3.3v15.3c0 .3.1.4.3.4h19.6c.2 0 .3-.1.3-.3V4.3c0-.1-.1-.3-.3-.3zm-1.6 13.4l-4.4-4.6c0-.1-.1-.1-.2 0l-3.1 2.7-3.9-4.8h-.1s-.1 0-.1.1L3.8 17V6h16.4v11.4zm-4.9-6.8c.9 0 1.6-.7 1.6-1.6 0-.9-.7-1.6-1.6-1.6-.9 0-1.6.7-1.6 1.6.1.9.8 1.6 1.6 1.6z"
            />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import _ from "lodash";
import { mapGetters } from "vuex";

export default {
  name: "NewPost",
  computed: {
    ...mapGetters({
      authUser: "authUser",
    }),
    postMessage: {
      get() {
        return this.$store.getters.postMessage;
      },
      set: _.debounce(function (postMessage) {
        this.$store.commit("updateMessage", postMessage);
      }, 300),
      // set(postMessage) {
      //   this.$store.commit("updateMessage", postMessage);
      // }
    },
  },
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>