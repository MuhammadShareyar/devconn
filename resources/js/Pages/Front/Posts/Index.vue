<template>
  <AppLayout>
    <Head title="Posts" />
    <section>
      <div class="">
        <Link :href="route('post.create')" class="btn btn-primary"
          >Create New Post</Link
        >
      </div>

      <div class="posts" >
        <template v-if="posts.data.length > 0">
        <div
          class="post bg-white p-1 my-1"
          v-for="(post, key) in posts.data"
          :key="key"
        >
          <div>
            <Link :href="route('usersprofile.show', post.user_id)">
              <img
                class="round-img"
                src="https://www.gravatar.com/avatar/205e460b479e2e5b48aec07710c08d50?s=200"
                alt=""
              />
              <h4>{{ post.created_by }}</h4>
            </Link>
          </div>
          <div>
            <h3>{{ post.title }}</h3>
            <p class="my-1">{{ post.content }}</p>
            <p class="post-date">Posted on {{ post.created_at }}</p>
            <button
              type="button"
              class="btn btn-light"
              :class="{ active: post.liked }"
              @click="postLike(post.id,key)"
            >
              <i class="fas fa-thumbs-up"></i>
              <span v-if="post.likes_count">{{ post.likes_count }}</span>
            </button>
            <Link :href="route('post.show', post.id)" class="btn btn-primary">
              Discussion
              <span :class="{ 'comment-count': post.total_comments }">{{
                post.total_comments ? post.total_comments : ""
              }}</span>
            </Link>
            <button type="button" class="btn btn-danger" @click="deletePost(post.id)">
              <i class="fas fa-times"></i>
            </button>
          </div>
        </div>
        </template>
        <template v-else>
          <div style="text-align:center;box-shadow:0px 1px 6px 1px #c8cfcf;margin-top:30px">
            <h2 style="padding:20px"> No post available!</h2>
          </div>
        </template>
        <pagination :links="posts.links" />
      </div>
    </section>
  </AppLayout>
</template>
<script>
import { Head, Link } from "@inertiajs/inertia-vue";
import AppLayout from "../../../layouts/front/AppLayout.vue";
import axios from "axios";
export default {
  components: { Head, Link, AppLayout },
  props: {
    user: Object,
    posts: Object,
  },
  methods: {
    postLike(postId,itemKey) {
      axios.post(route("like.store"), { post_id: postId }).then((response) => {
        this.$inertia.reload({only:['posts']});
      });
    },
    deletePost(postId) {

      if(confirm('Are you sure?')){
        this.$inertia.delete(route("post.destroy", postId));
      }
    },
  },
};
</script>