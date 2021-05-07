<template>
  <div
    class="friend"
    v-for="personalDetail in personalDetails"
    :key="personalDetail.id"
  >
    <img :src="personalDetail.profileImage" alt="user 1" />
    <img v-if="personalDetail.image" :src="imageUrlFor(personalDetail.image)" />
    <p>{{ personalDetail.firstname }}</p>
    <button type="submit">View</button>
  </div>
</template>

<script>
export default {
  name: "contact",
  props: {
    personalDetails: Array,
  },
};
</script>

<style scoped>
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
