<template>
  <div class="personalDetails">
    <div class="loading" v-if="loading">Loading...</div>

    <div v-if="error" class="error">
      {{ error }}
    </div>
    <div>
      <p class="back">&#x3c; Back</p>
    </div>
    <div class="main" v-if="personalDetail">
      <div class="container">
        <img
          v-if="personalDetail.image"
          :src="imageUrlFor(personalDetail.image)"
          class="pic"
        />
        <div class="content">
          <p class="name">
            {{ personalDetail.firstname }} {{ personalDetail.lastname }}
          </p>
          <p class="nickname">{{ personalDetail.nickname }}</p>
          <div class="main-info">
            <p class="bio">
              <span class="label">Description</span><br />
              {{ personalDetail.excerpt }}
            </p>
            <p class="phone-number">
              <span class="label">Phone Number</span><br />
              {{ personalDetail.phoneNumber }}
            </p>
            <p class="age">
              <span class="label">D.O.B</span><br />
              {{ personalDetail.birthmonth }} {{ personalDetail.birthday }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import sanity from "../client";
import imageUrlBuilder from "@sanity/image-url";

const imageBuilder = imageUrlBuilder(sanity);

const query = `*[slug.current == $slug]{
  _id,
  firstname,
  lastname,
  nickname,
  slug,
  birthday,
  phoneNumber,
  birthmonth,
  "image": profileImage{
  asset->{
  _id,
  url
}
},
  categories,
  excerpt
}[0]
`;

export default {
  name: "PersonalDetails",
  data() {
    return {
      loading: true,
      personalDetail: [],
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
      sanity.fetch(query, { slug: this.$route.params.slug }).then(
        (personalDetail) => {
          this.loading = false;
          this.personalDetail = personalDetail;
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
.personalDetails {
  height: 100%;
}

.back {
  color: rgba(0, 0, 0, 0.5);
  font-weight: bold;
  font-size: 13px;
  padding: 5%;
}

.main {
  height: 80%;
  position: absolute;
  background-color: #d6d6d6;
  width: 100%;
  bottom: 0;
  z-index: 1;
  border-top-left-radius: 30px;
  border-top-right-radius: 30px;
}

.container {
  height: 100%;
  width: 100%;
  position: relative;
}

.pic {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 4px solid #5c3fd7;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: -50px;
}

.content {
  padding-top: 50px;
  width: 100%;
}

.content .name {
  text-align: center;
  font-size: 18px;
  font-weight: bold;
  margin: 5px 0 0;
}

.content .nickname {
  color: rgba(0, 0, 0, 0.5);
  font-weight: bold;
  font-size: 14px;
  text-align: center;
}

.main-info {
  padding: 20px;
}

.main-info p {
  margin: 15px 0;
  font-size: 16px;
  color: rgba(0, 0, 0, 0.925);
}

.main-info p span {
  font-weight: bold;
  color: #000;
}

.main-info p span::after {
  content: ":";
}
</style>
