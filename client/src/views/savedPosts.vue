<template>
  <div class="container">
    <h1 class="latest-posts-h1">Saved Posts</h1>
    <hr />
    <div class="row">
      <div id="card" class="card" v-for="post in posts" :key="post._id">
        <img
          style="height: 180px;"
          class="card-img-top"
          :src="post.imageUrl"
          alt="Card image cap"
        />
        <div class="card-body">
          <h5 class="card-title">{{ post.title }}</h5>

          <p class="card-text">
            {{ post.description.slice(0, 30) + "..." }}
          </p>

          <router-link
            class="btn btn-dark card-link"
            style="float: left; width: 100%;"
            :to="`/details/${post._id}`"
            >Details</router-link
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import store from "../store";
import postServices from "../services/postServices";

export default {
  name: "home",
  data() {
    return {
      posts: [],
    };
  },
  async created() {
    store.commit("getsavedposts_request");
    postServices.getSavedPosts().then((res) => {
      res.data.forEach((postId) => {
        postServices.getOne(postId).then((result) => {
          this.posts.push(result.data);
        });
      });
    });
  },
};
</script>

<style scoped>
.row {
  justify-content: space-around;
}
.card {
  width: 22rem;
  margin-top: 20px;
}

.latest-posts-h1 {
  margin-top: 10px;
  margin-bottom: 40px;
  text-align: center;
}

router-link {
  border-radius: 30px;
}
</style>
