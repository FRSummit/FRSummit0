<template>
  <div class="name-section">
    <div v-for="(info, i) in sectionInfo" :key="i">
      <div class="left-section">
        <p class="my-name">{{ info.name }}</p>
        <p class="my-address">
          Address: {{ info.address }}
        </p>
        <p class="my-email">Email: {{ info.email }}</p>
        <p class="my-phone">Phone: {{ info.phone }}</p>
      </div>
      <div class="right-section">
        <img src="../../../../assets/images/FRS.jpg" alt="FRSummit" />
      </div>
    </div>
    <div v-if="!sectionInfo.TopSection">
      <div class="left-section">
        <p class="my-name">Fayazur Rahman Summit</p>
        <p class="my-address">
          Address: Block A, Road 1, House 62/C, Bashundhara, Dhaka 1229
        </p>
        <p class="my-email">Email: www.frsummit1@gmail.com</p>
        <p class="my-phone">Phone: 01717627896, 01687858300</p>
      </div>
      <div class="right-section">
        <img src="../../../../assets/images/FRS.jpg" alt="FRSummit" />
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase";
export default {
  data() {
    return {
      sectionInfo: [],
    };
  },
  created() {
    firebase
      .database()
      .ref("TopNameAddressSection")
      .on("value", (snapshot) => {
        for (let i = 0; i < Object.keys(snapshot.val()).length; i++) {
          if (
            snapshot.val()[Object.keys(snapshot.val())[i]].TopSection.isSelected
          ) {
            this.sectionInfo = snapshot.val()[Object.keys(snapshot.val())[i]];
          }
          // console.log(Object.keys(snapshot.val())[i])
          // console.log(snapshot.val()[Object.keys(snapshot.val())[i]].TopSection.isSelected)
        }
      });
  },
};
</script>

<style scoped>
.name-section {
  overflow: hidden;
}
.left-section {
  float: left;
  text-align: left;
  overflow: hidden;
  width: 50%;
  margin-top: 50px;
}
.left-section p {
  margin: 0;
}
.left-section .my-name {
  font-size: 20px;
  font-weight: bold;
}
.left-section .my-address {
  font-size: 16px;
}
.left-section .my-email {
  font-size: 16px;
}
.left-section .my-phone {
  font-size: 16px;
}
.right-section {
  float: right;
  overflow: hidden;
  width: 138px;
}
.right-section img {
  width: 128px;
  height: 150px;
  margin-top: 4px;
  box-shadow: 0 1px 6px 0px #272727;
}
</style>