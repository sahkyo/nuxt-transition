<template>
  <div class="container">
    <nuxt-link to="/article">
      <div class="city paris" ref="wrapper">
        <img
          src="https://images.unsplash.com/photo-1502602898657-3e91760cbb34?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2852&q=80"
          alt="paris"
          ref="img"
        />
      </div>
    </nuxt-link>
    <div class="thumbnails" ref="others">
      <div class="city london">
        <img
          src="https://images.unsplash.com/photo-1514557718210-26e452f8fab0?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80"
          alt="london"
        />
      </div>
      <div class="city ny">
        <img
          src="https://images.unsplash.com/photo-1518235506717-e1ed3306a89b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80"
          alt="new york"
        />
      </div>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  data() {
    return {
      aspectRatio: null,
      thumbnailWidth: 340,
      thumbnailHeight: 589,
      coverWidth: null,
      coverHeight: null
    };
  },

  mounted() {
    this.aspectRatio = this.$refs.img.naturalWidth / this.$refs.img.naturalHeight;
    this.coverHeight = this.$refs.wrapper.getBoundingClientRect().height;

    this.setup();
    
    if (process.client) {
      window.addEventListener("resize", this.setup);
    }
  },

  methods: {
    setup() {
      this.coverWidth = window.innerWidth;

      const proportions = {
        scaleX: (this.thumbnailWidth / this.coverWidth) * this.aspectRatio,
        scaleY: this.thumbnailHeight / this.coverHeight,
        y: window.innerHeight / 2 - this.coverHeight / 2,
      };

      gsap.set(this.$refs.wrapper, {
        scaleX: proportions.scaleX,
        scaleY: proportions.scaleY,
        y: proportions.y,
      });

      gsap.set(this.$refs.img, {
        scaleX:
          (((1 / proportions.scaleX) * this.thumbnailWidth) /
            this.$refs.img.clientHeight) *
          this.aspectRatio,
        scaleY:
          ((1 / proportions.scaleY) * this.thumbnailHeight) /
          this.$refs.img.clientHeight,
      });
    }
  },

  transition: {
    css: false,
    mode: "out-in",
    enter(el, done) {
      gsap.from(el, {
        autoAlpha: 0,
      });
    },
    leave(el, done) {
      gsap
        .timeline()
        .to(".thumbnails", {
          autoAlpha: 0,
        })
        .to(
          ".paris img",
          {
            scaleX: 1,
            scaleY: 1,
            ease: "expo.inOut",
            duration: 1,
          },
          0
        )

        .to(
          ".paris",
          {
            y: 0,
            scaleX: 1,
            scaleY: 1,
            ease: "expo.inOut",
            duration: 1,
            onComplete: done,
          },
          0
        );
    },
  },
};
</script>
