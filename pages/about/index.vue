<template>
  <div class="has-background-primary-off">
    <Nav color="has-background-primary" />
    <div class="fullscreen">
      <article class="section container">
        <div class="max-width-78ch">
          <h1 class="section-title is-flex is-align-items-center">
            <img src="~/assets/images/me.jpg" class="me" />
            <span style="margin-left: 1rem">About Me</span>
          </h1>
          <p>
            Hey, I'm Dyllon! I'm a consultant, investor, and entrepreneur based
            in Houston, Texas. I am currently working for Oliver Wyman in
            Management Consulting.
          </p>
          <p>
            I am extremely passionate about my current entrepreneurial venture,
            Xplor. My co-founder, Brandon Cua, and I are dedicated to
            democratizing career and life mentorship for students of all
            backgrounds. We are creating a social platform to provide the
            guidance and resources missed by current services impacting this
            space.
          </p>
        </div>
      </article>
    </div>
    <Footer />
  </div>
</template>

<script>
import getSiteMeta from "~/utils/getSiteMeta.js";

export default {
  computed: {
    meta() {
      const metaData = {
        url: `${this.$config.baseURL}/about`,
      };
      return getSiteMeta(metaData);
    },
  },
  head() {
    return {
      title: "About | Dyllon Schmehl",
      meta: [...this.meta],
      link: [
        {
          hid: "canonical",
          rel: "canonical",
          href: `${this.$config.baseURL}/about`,
        },
      ],
    };
  },
};
</script>

<style scoped>
.me {
  max-width: 100px;
  border-radius: 50%;
}

p {
  font-size: 1.2rem;
}

p:not(:last-of-type) {
  margin-bottom: 1rem;
}
</style>
