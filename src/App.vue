<template>
  <div id="app-root">
    <span class="material-icons-round icon" @click="turnLeft">
      chevron_left
    </span>
    <h1 id="no-nft" v-if="nfts.length<=0">No NFT here.</h1>
    <CardComponent v-else id="card" :nft="nftShow" :show-image="showImage" />
    <span class="material-icons-round icon" @click="turnRight">
      chevron_right
    </span>
    <ImageViewer id="img-viewer" :image="img.src" :close="closeImage" />
  </div>
  <p id="no-small-screen">Not adapted for phone screen.</p>
</template>

<script>
import $ from 'jquery'
import CardComponent from "@/components/CardComponent"
import ImageViewer from "@/components/ImageViewer";

export default {
  name: 'App',
  components: {ImageViewer, CardComponent},
  data() {
    return {
      nfts: [],
      nftShow: {},
      index: 0,
      img: {
        src: ''
      }
    }
  },
  methods: {
    turnLeft() {
      this.index--
      if (this.index<0)
        this.index = this.nfts.length-1

      let card = $("#card")
      card.animate({
        opacity: 0
      })
      setTimeout(() => {
        this.nftShow = this.nfts[this.index]
        card.animate({
          opacity: 1
        })
      }, 650)
    },
    turnRight() {
      this.index++
      if (this.index>=this.nfts.length)
        this.index = 0

      let card = $("#card")
      card.animate({
        opacity: 0
      })
      setTimeout(() => {
        this.nftShow = this.nfts[this.index]
        card.animate({
          opacity: 1
        })
      }, 650)
    },
    closeImage() {
      $("#img-viewer").fadeOut()
    },
    showImage(src) {
      this.img.src = src
      $("#img-viewer").fadeIn()
    }
  },
  mounted() {
    this.nfts = require("@/assets/nfts.json")
    this.nftShow = this.nfts[0]
    $("#img-viewer").hide()
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Barlow+Semi+Condensed:ital,wght@0,400;0,500;0,700;0,900;1,500&family=Fredoka:wght@400;500;600&display=swap');
@import url('https://fonts.googleapis.com/icon?family=Material+Icons+Round');

:root {
  --soft-blue: hsl(215, 51%, 70%);
  --cyan: hsl(178, 100%, 50%);

  --very-dark-blue: hsl(215, 32%, 20%);
  --dark-blue: hsl(216, 50%, 16%);
  --blue: hsl(215, 32%, 27%);
  --white: hsl(0, 0%, 100%);
}

html, body, #app, #app-root {
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
}

#app {
  font-family: "Barlow Semi Condensed", sans-serif;
  background-color: var(--very-dark-blue);
}

#app-root {
  display: flex;
  align-items: center;
  justify-content: center;
}

p {
  font-size: 18px;
}

a {
  text-decoration: none;
}

span.icon {
  font-size: 80px;
  color: var(--soft-blue);
  cursor: pointer;
  background-color: var(--dark-blue);
  border-radius: 100%;
  margin: 1rem;
  transition: all 0.3s ease-in-out;
  user-select: none;

  &:hover {
    transform: scale(1.2);
    box-shadow: white 0 0 10px;
  }
}
#no-nft {
  color: var(--soft-blue);
}

@media screen and (max-width: 620px), screen and (max-height: 600px) {
  #app-root {
    display: none;
  }
  #no-small-screen {
    color: var(--white);
  }
  #app {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
