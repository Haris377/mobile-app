<template>
  <view class="container">
    <image class="backImage" :source="images[currentImage]" />
    <!-- <Image source={"this.image} /> -->
    <!-- <view
      :style="{
        position: 'absolute',
        top: 0,
        left: 0,
        right: 0,
        bottom: 0,
        justifyContent: 'center',
        alignItems: 'center',
      }"
    >
      <button
        :on-press="next"
        title="Learn More"
        color="#841584"
        accessibility-label="Learn more about this purple button"
      />
    </view> -->
    <view class="footer">
      <nb-button class="btn" :on-press="skip" transparent>
        <nb-text :style="{color: 'white'}">Skip</nb-text>
      </nb-button>
      <nb-button class="btn" :on-press="next" iconRight transparent>
        <nb-text :style="{color: 'white'}">Next</nb-text>
        <nb-icon :style="{color: 'white'}" active name="arrow-forward" />
      </nb-button>
    </view>
  </view>
</template>

<script>
import {StatusBar} from 'react-native';
export default {
  components: {},
  data() {
    return {
      currentImage: 0,
      images: [
        require('../assets/q.png'),
        require('../assets/linear.png'),
        require('../assets/q2.jpg'),
        require('../assets/q3.jpg'),
      ],
    };
  },
  props: {
    navigation: {
      type: Object,
    },
  },
  methods: {
    next() {
      if (this.currentImage < this.images.length - 1) {
        this.currentImage = this.currentImage + 1;
      } else {
        this.navigation.navigate('Login');
      }
      return this.currentImage;
    },
    skip() {
      this.navigation.navigate('Login');
    },
  },
  mounted() {
    console.log('mount');
    StatusBar.setBarStyle('dark-content');
    Platform.OS === 'android' && StatusBar.setBackgroundColor('transparent');
    StatusBar.setTranslucent(true);
  },
};
</script>

<style>
.container {
  height: 100%;
}
.backImage {
  width: 100%;
  height: 100%;
}
.title {
  margin: auto;
  text-align: center;
  margin-top: 50%;
  color: black;
  font-size: 22;
}
.footer {
  position: absolute;
  justify-content: space-between;
  left: 0;
  right: 0;
  bottom: 0;
  height: 60;
  background-color: 'rgba(52, 52, 52, 0.3)';
  flex-direction: row;
}
.btn {
  margin-top: 7;
  justify-content: center;
  align-items: center;
}
</style>
