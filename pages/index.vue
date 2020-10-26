<template>
  <div class="container">
    <nuxt-link to="/article">
      <div class="city paris">
        <img src="@/assets/img/paris.jpg" alt="" />
      </div>
    </nuxt-link>
    <div class="thumbnails">
      <div class="city london">
        <img src="@/assets/img/london.jpg" alt="" />
      </div>
      <div class="city ny">
        <img src="@/assets/img/ny.jpg" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  data() {
    return {
      link: null,
      img: null,
      aspect: null,
      rect: null,
      thumbnailWidth: 340,
      thumbnailHeight: 589
    };
  },

  mounted() {
    this.setup();

    if (process.client) {
      window.addEventListener("resize", () => {
        const proportions = {
          scaleX: (this.thumbnailWidth / window.innerWidth) * this.aspect,
          scaleY: this.thumbnailHeight / 537,
          y: window.innerHeight / 2 - this.rect.top - this.rect.height / 2
        };

        gsap.set(this.link, {
          scaleX: proportions.scaleX,
          scaleY: proportions.scaleY,
          y: proportions.y
        });

        gsap.set(this.img, {
          scaleX:
            (((1 / proportions.scaleX) * this.thumbnailWidth) /
              this.img.clientHeight) *
            this.aspect,
          scaleY:
            ((1 / proportions.scaleY) * this.thumbnailHeight) /
            this.img.clientHeight
        });
      });
    }
  },

  methods: {
    setup() {
      this.link = document.querySelector(".paris");
      this.img = this.link.querySelector("img");
      this.aspect = this.img.naturalWidth / this.img.naturalHeight;
      this.rect = this.link.getBoundingClientRect();

      const proportions = {
        scaleX: (this.thumbnailWidth / window.innerWidth) * this.aspect,
        scaleY: this.thumbnailHeight / 537,
        y: window.innerHeight / 2 - this.rect.top - this.rect.height / 2
      };

      gsap.set(this.link, {
        scaleX: proportions.scaleX,
        scaleY: proportions.scaleY,
        y: proportions.y
      });

      gsap.set(this.img, {
        scaleX:
          (((1 / proportions.scaleX) * this.thumbnailWidth) /
            this.img.clientHeight) *
          this.aspect,
        scaleY:
          ((1 / proportions.scaleY) * this.thumbnailHeight) /
          this.img.clientHeight
      });
    }
  },

  transition: {
    css: false,
    mode: "out-in",
    enter(el, done) {
      gsap.from(el, {
        autoAlpha: 0
      })
    },
    leave(el, done) {
      gsap
        .timeline()
        .to(".london", {
          autoAlpha: 0
        })
        .to(
          ".ny",
          {
            autoAlpha: 0
          },
          0
        )
        .to(
          ".paris img",
          {
            scaleX: 1,
            scaleY: 1,
            ease: "expo.inOut",
            duration: 1
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
            onComplete: done
          },
          0
        );
    }
  }
};
</script>
