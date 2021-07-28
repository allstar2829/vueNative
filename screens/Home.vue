<template>
  <view class="container">
    <image class="top-bg" :source="require('./countrylist-bg.jpg')" />
    <text class="title">COUNTRY LIST</text>
    <view class="d-flex" :style="{paddingBottom:20 ,borderBottomWidth: 1, borderBottomColor: 'gray'}">
      <text-input
        :style="{
          height: 30,
          width: '70%',
          borderColor: 'lightgray',
          borderWidth: 1,
          borderRadius: 8,
          padding: 5,
        }"
        v-model="text"
        placeholder="Search here..."
      />
      <!-- <button :on-press="searchItem" title="Search" class="btnSearch" /> -->
      <touchable-opacity
        :on-press="searchItem"
        :style="{ backgroundColor: 'gray', padding: 8, borderRadius: 8, marginLeft: 10 }"
      >
        <text :style="{ color: 'white' }">Search</text>
      </touchable-opacity>
    </view>
    <scroll-view class="scroll-area">
      <view
        v-for="(country, index) in countries"
        :key="index"
        :style="{ padding: 10}"
      >
        <touchable-opacity class="d-flex" :on-press="onPressButton">
          <!-- <image
            :style="{ width: 25, height: 25, borderRadius: 25, marginRight: 8 }"
            :source="{
              uri: 'country.flag',
            }"
            :source="{uri: country.flag}"
          /> -->
          <image
            :style="{ width: 25, height: 25, borderRadius: 25, marginRight: 8 }"
            :source="{
              uri: 'https://facebook.github.io/react-native/docs/assets/favicon.png',
            }"
          />
          <text class="item-style">{{ country.name }}</text>
        </touchable-opacity>
      </view>
    </scroll-view>
    <touchable-opacity
        :on-press="() => nextPage()"
        :style="{ backgroundColor: 'black', padding: 8, width: '100%'}"
      >
        <text :style="{ color: 'white' }">NEXT PAGE</text>
      </touchable-opacity>
  </view>
</template>

<script>

export default {
  data() {
    return {
      text: "",
      countries: [],
    };
  },
    props: {
    navigation: {
      type: Object
    }
  },
  mounted() {
    fetch("https://restcountries.eu/rest/v2/all")
      .then((response) => response.json())
      .then((data) => {
        // console.log(data);
        this.countries = data;
      });
  },
  methods: {
    onPressButton() {
      // console.log();
      alert("test");
    },
    searchItem() {
      console.log("test");
    },
    nextPage(){
      this.navigation.navigate('DetailsScreen');
    },
  },
};
</script>

<style>
/* useless  */

/* *{
  outline: 1px solid red;
} */
/* display: block; */
/* border-bottom:1px solid lightgray;/ */

.container {
  flex: 1;
  background-color: rgb(255, 255, 255); 
  align-items: center;
  justify-content: center;
  /* position: absolute;
  top: 0;
  left: 0; */
}
.d-flex {
  flex-direction: row;
  align-items: center;
}
.top-bg {
  /* display: block; */
  width: 100%;
  height: 100;
  position: relative;
  top: 0;
  left: 0;
}
.title {
  color: gray;
  padding: 10;
  font-size: 32px;
  /* position: absolute;
  top: 0;
  left: 0; */
}
.scroll-area {
  width: 100%;
  max-height: 500;
}
.item-style {
  width: 100%;
  padding: 15;
  /* border-bottom:1px solid lightgray;/ */
}
.btnSearch {
  background-color: black;
  padding: 5;
  color: white;
  border-radius: 10;
}

</style>