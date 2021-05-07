<template>
  <div class="personalDetails">
    <div>
      <p class="back">&#x3c; Back</p>
    </div>
    <div class="main">
      <div class="container">
        <img src="@/assets/user1.jpg" alt="" class="pic" />
        <div class="content">
          <p class="name">Joel Olawanle</p>
          <p class="nickname">Tobest</p>
          <div class="main-info">
            <p class="bio">
              <span class="label">Description</span><br />
              Lorem ipsum dolor sit amet, consectetur adipisicing elit.
              Voluptatem nihil culpa praesentium, ea minima hic non magni!
              Aspernatur esse autem corporis totam numquam. Odio, beatae facere
              non autem omnis dicta?
            </p>
            <p class="phone-number">
              <span class="label">Phone Number</span><br />
              07035522621
            </p>
            <p class="age">
              <span class="label">Age</span><br />
              10
            </p>
            <p class="religion">
              <span class="label">Religion</span><br />
              Christian
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Personal Details",
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
