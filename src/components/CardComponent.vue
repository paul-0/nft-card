<template>
  <div id="card" @mouseleave="toggleDescription" @mouseenter="toggleDescription">
    <div id="nft">
      <div id="img" @mouseleave="hoverImageOut" @mouseenter="hoverImage">
        <img id="nft-img" :src="getSrc(image)" alt="NFT image">
        <span id="icon-view">
          <img src="../assets/images/icon-view.svg" alt="">
        </span>
      </div>
      <h3 class="text-hover-cyan">{{title}} {{id}}</h3>
      <div id="info">
        <p id="description">{{description}}</p>
        <span>
          <span id="price">
            <img src="../assets/images/icon-ethereum.svg"  alt="Icon of Ethereum"/>
            <span>{{price}}</span>
          </span>
          <span>
            <img src="../assets/images/icon-clock.svg"  alt=""/>
            <span>{{getDayLeft()}} days left</span>
          </span>
        </span>
      </div>
    </div>
    <div id="creator">
      <img id="avatar" :src="getSrc(creator.avatar)" alt="Creator avatar">
      Creation of<span class="text-hover-cyan">{{creator.name}}</span>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'

export default {
  name: "CardComponent",
  data() {
    return {
      id: "#3429",
      title: "Equilibrium",
      description: "Our Equilibrium collection promotes balance and calm",
      image: "image-equilibrium.jpg",
      price: "0.041 ETH",
      expireDate: new Date(Date.now() + (1000 * 60 * 60 * 24 * 3)),
      creator: {
        name: "Jules Wyvern",
        avatar: "image-avatar.png"
      }
    }
  },
  methods: {
    getDayLeft() {
      return Math.round((this.expireDate.getTime() - Date.now()) / (1000 * 60 * 60 * 24));
    },
    getSrc(img) {
      if (img)
        return require('../assets/images/' + img);
      else return "";
    },
    toggleDescription() {
      $('#info').animate({
        height: 'toggle'
      }, 300)
    },
    hoverImage() {
      $("#icon-view").fadeIn()
    },
    hoverImageOut() {
      $("#icon-view").fadeOut()
    }
  },
  mounted() {
    $("#info").hide();
    $("#icon-view").hide();
  }
}
</script>

<style scoped lang="scss">
#card {
  background-color: var(--dark-blue);
  color: var(--soft-blue);
  padding: 1rem;
  width: 350px;
  max-height: 600px;
  border-radius: 1rem;
  position: relative;
  transition: all 0.3s ease-in-out;

  &:hover {
    transform: scale(1.05);
  }
}

#nft {
  h3 {
    font-size: 1.5rem;
    color: var(--white);
    margin-bottom: 0;
    cursor: pointer;
  }
  #description {
    margin-bottom: 0;
  }
  #info > span {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 1rem;
    font-weight: bold;
    background-color: var(--dark-blue);

    span {
      display: flex;
      gap: 0.5rem;
    }
    #price {
      color: var(--cyan);
    }
  }

  #img {
    position: relative;
    cursor: pointer;

    * {
      border-radius: 1rem;
    }
    #nft-img {
      width: 100%;
      height: 100%;
    }

    #icon-view {
      position: absolute;
      background-color: transparentize(hsl(178, 100%, 50%), 0.5);
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;

      img {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        height: 5rem;
      }
    }
  }
}

#creator {
  display: flex;
  align-items: center;
  gap: 1rem;
  border-top: var(--blue) 1px solid;
  padding-top: 1rem;
  margin-top: 1rem;

  #avatar {
    height: 50px;
    border: white solid 1px;
    border-radius: 100%;
  }
  span {
    color: var(--white);
    font-weight: bold;
    margin-left: -10px;
    cursor: pointer;
  }
}

.text-hover-cyan:hover {
  color: var(--cyan) !important;
}

</style>