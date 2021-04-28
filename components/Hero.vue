<template>
  <section
    class="hero has-background-primary has-background-primary-gradient is-fullheight"
  >
    <div class="hero-body">
      <div class="is-flex responsive-flex prevent-shifting">
        <div class="half-flex responsive-margin">
          <div>
            <div>
              <h2 class="subtitle heading is-size-5">
                Consulting, Investing, and Entrepreneurship
              </h2>
              <h1 class="title is-size-huge has-text-weight-bold">
                Hi, I'm
                <span
                  @click="showAbout = !showAbout"
                  class="has-text-weight-boldest link"
                  >Dyllon Schmehl</span
                >!
              </h1>
              <p class="is-size-5 content max-width-78ch">
                Read some of my
                <NuxtLink :to="{ path: '/post' }" class="link py-1"
                  >blog posts</NuxtLink
                >.
              </p>
            </div>
          </div>
        </div>
        <div class="half-flex prevent-jitter">
                    <!-- https://vuejs.org/v2/guide/transitions.html#Transition-Modes -->
                    <transition name="fade" mode="out-in">
                        
            <div v-if="showAbout" key="text">
                            
              <p class="has-text-centered is-size-5 content max-width-78ch">
                Academically curious with a hunger for success.
              </p>
                          
            </div>
                        
            <div v-else class="has-text-centered" key="image">
                            <img
                src="~assets/images/me.jpg"
                alt="An image of Dyllon Schmehl"
                class="me"
                @click="showAbout = !showAbout"
              />
                          
            </div>
                      </transition
          >
                  
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      showAbout: false,
    };
  },
  computed: {},
  methods: {},
};
</script>

<style lang="scss" scoped>
h1,
h2,
p,
span,
a {
  &::selection {
    background: $secondary;
    color: $primary;
  }
}

a {
  color: $text;
}

.is-size-huge {
  font-size: 4rem;

  @media screen and (max-width: 860px) {
    font-size: 3rem;
  }
}

.responsive-margin {
  @media screen and (min-width: 860px) {
    margin-right: 1rem;
    margin-left: 1rem;
  }

  @media screen and (max-width: 860px) {
    margin-bottom: 3rem;
  }
}

@media screen and (max-width: 860px) {
  .prevent-jitter {
    min-height: 200px;
  }
}

.half-flex {
  flex: 1 1 0px;
  width: 100%;
}

.responsive-flex {
  flex-direction: row;
  align-items: center;

  @media screen and (max-width: 860px) {
    flex-direction: column;
    align-items: flex-start;
  }
}

.prevent-shifting {
  width: 100%;
}

.me {
  width: 250px;
  height: 250px;
  border-radius: 0.5rem;
  transition: all 1s ease;
  /* offset-x | offset-y | blur-radius | color */
  box-shadow: 3px 3px 4px #6a0788;
  &:hover {
    transform: scale(0.95);
    box-shadow: 0px 0px 25px white;
    cursor: pointer;
  }
}
</style>
