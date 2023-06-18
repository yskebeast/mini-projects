<template>
  <fs-project-container title="star rating">
    <div class="star-rating">
      <div class="main">
        <div class="container">
          <div class="star-container">
            <div class="star"></div>
            <span class="number">1</span>
          </div>

          <div class="star-container">
            <div class="star"></div>
            <span class="number">2</span>
          </div>

          <div class="star-container">
            <div class="star"></div>
            <span class="number">3</span>
          </div>

          <div class="star-container">
            <div class="star"></div>
            <span class="number">4</span>
          </div>
        </div>
      </div>
    </div>
  </fs-project-container>
</template>

<script>
export default {
  name: "star-rating",
  data() {
    return {};
  },
  computed: {},
  methods: {},
  mounted() {
    const starContainer = document.querySelectorAll(".star-container");
    starContainer.forEach((star, pos) => {
      star.addEventListener("click", () => {
        if (!star.classList.contains("active")) {
          for (let i = 0; i <= pos; i++) {
            starContainer[i].classList.add("active");
          }
        } else {
          for (let i = pos + 1; i <= starContainer.length - 1; i++) {
            starContainer[i].classList.remove("active");
          }
        }
      });
    });
  },
};
</script>

<style lang="scss" scoped>
.star-rating {
  padding: 3rem 0;
  height: 100vh;
  background-color: #ececec;
}

.main {
  width: 40em;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  display: flex;
  justify-content: space-between;
  gap: 3rem;
}
.star-container {
  cursor: pointer;
  outline: 1px solid red;
  width: 5rem;
  height: 5rem;
  &.active {
    background: yellow;
  }
}

.star {
  width: 100%;
  height: 100%;
  outline: 1px solid red;
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
  // &.active {
  //   background: yellow;
  // }
}
</style>
