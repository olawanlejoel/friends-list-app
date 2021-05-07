<template>
  <div class="home">
    <div class="head-info">
      <p class="title">Welcome!</p>
      <p class="sm-text">
        You currently have
        <strong>{{ personalDetails.length }}</strong> Friend(s).
      </p>
    </div>
    <div class="friends-area">
      <p class="sm-title">Friend(s)</p>
      <div class="friends">
        <div
          class="friend"
          v-for="personalDetail in personalDetails"
          :key="personalDetail.id"
        >
          <img
            v-if="personalDetail.image"
            :src="imageUrlFor(personalDetail.image)"
          />
          <p>{{ personalDetail.firstname }} {{ personalDetail.lastname }}</p>
          <router-link :to="`/personalDetails/${personalDetail.slug.current}`">
            <button>View</button>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import sanity from "../client";

import imageUrlBuilder from "@sanity/image-url";

const imageBuilder = imageUrlBuilder(sanity);

const query = `*[_type == "personalDetail"]{
  _id,
  firstname,
  lastname,
  slug,
  "image": profileImage{
  asset->{
  _id,
  url
}
}
}[0...50]`;

export default {
  name: "Home",
  data() {
    return {
      loading: true,
      personalDetails: [],
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    imageUrlFor(source) {
      return imageBuilder.image(source);
    },
    fetchData() {
      this.error = this.personalDetail = null;
      this.loading = true;
      sanity.fetch(query).then(
        (personalDetails) => {
          this.loading = false;
          this.personalDetails = personalDetails;
        },
        (error) => {
          this.error = error;
        }
      );
    },
  },
};
</script>

<style scoped>
.home {
  padding: 30px 20px;
}
.head-info .title {
  font-size: 24px;
  font-weight: bold;
}

.head-info .sm-text,
.sm-title {
  font-size: 14px;
  color: rgb(63, 63, 63);
}

.friends-area {
  margin-top: 30px;
}

.friend {
  display: flex;
  align-items: center;
  justify-content: space-around;
  margin-top: 10px;
  border-bottom: 1px solid rgba(161, 161, 161, 0.589);
  padding: 10px 0;
}

.friend:last-child {
  border-bottom: none;
  margin-bottom: 50px;
}

.friend img {
  width: 50px;
  max-width: 100%;
  height: 50px;
  border-radius: 50%;
  border: 2px solid #5c3fd7;
}

.friend button {
  padding: 10px 20px;
  border: none;
  background-color: #5c3fd7;
  color: #fff;
  border-radius: 20px;
}
</style>
