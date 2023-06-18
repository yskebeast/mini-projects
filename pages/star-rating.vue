<template>
  <fs-project-container title="star rating">
    <div class="star-rating">
      <div class="main">
        <div class="container">
          <div class="message"></div>
          <div class="star-container">
            <div class="star" />
            <span class="number">1</span>
          </div>

          <div class="star-container">
            <div class="star" />
            <span class="number">2</span>
          </div>

          <div class="star-container">
            <div class="star" />
            <span class="number">3</span>
          </div>

          <div class="star-container">
            <div class="star" />
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
    const message = document.querySelector(".message");
    starContainer.forEach((container, pos) => {
      container.addEventListener("click", () => {
        if (!container.classList.contains("active")) {
          for (let i = 0; i <= pos; i++) {
            starContainer[i].classList.add("active");
          }
        } else {
          for (let i = pos + 1; i <= starContainer.length - 1; i++) {
            starContainer[i].classList.remove("active");
          }
        }

        message.innerHTML = "rate";
        const active = document.querySelectorAll(".active");
        if (active.length === 1) {
          console.log(1);
          message.innerHTML = "ter";
        } else if (active.length === 2) {
          console.log(2);
          message.innerHTML = "bad";
        } else if (active.length === 3) {
          console.log(3);
          message.innerHTML = "good";
        } else if (active.length === 4) {
          console.log(4);
          message.innerHTML = "exe";
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
}

.star {
  width: 100%;
  height: 100%;
  outline: 1px solid red;
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}

.star-container.active {
  & .star {
    background: yellow;
  }
}
</style>
