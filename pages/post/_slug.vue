<template>
  <div class="has-background-primary-off">
    <Nav color="has-background-primary" />
    <article class="section max-width-78ch mt-6">
      <h1 class="title has-text-weight-boldest is-size-2 is-size-4-mobile">
        {{ post.title }}
      </h1>
      <h2 class="subtitle heading is-size-6 has-text-weight-light">
        {{ formatDate(post.date) }}
      </h2>
      <p class="subtitle is-size-5 is-size-6-mobile">
        {{ post.description }}
      </p>
      <hr />

      <nuxt-content :document="post" />
      <hr />
      <div class="my-4">
        <NuxtLink
          to="/post"
          class="subtitle has-text-weight-light is-size-5 link heading is-inline-block"
          >👈 Back to all posts</NuxtLink
        >
      </div>
      <prev-next :prev="prev" :next="next" type="post" />
    </article>
    <Footer />
  </div>
</template>

<script>
import getSiteMeta from "~/utils/getSiteMeta.js";

export default {
  async asyncData({ $content, params }) {
    const post = await $content("posts", params.slug).fetch();

    const [prev, next] = await $content("posts")
      .only(["title", "slug", "img", "img_alt"])
      .sortBy("date", "asc")
      .surround(params.slug)
      .fetch();

    return { post, prev, next };
  },
  methods: {
    formatDate(date) {
      const options = { year: "numeric", month: "long" };
      return new Date(date).toLocaleDateString("en", options);
    },
  },
  computed: {
    meta() {
      const metaData = {
        type: "article",
        title: this.post.title,
        description: this.post.description,
        url: `${this.$config.baseURL}/post/${this.$route.params.slug}`,
        mainImage: `${this.$config.baseURL}/post/${this.post.img}`,
      };
      return getSiteMeta(metaData);
    },
  },
  head() {
    return {
      title: `${this.post.title} | Dyllon Schmehl`,
      meta: [
        ...this.meta,
        {
          property: "article:published_time",
          content: this.post.createdAt,
        },
        {
          property: "article:modified_time",
          content: this.post.updatedAt,
        },
        { name: "twitter:label1", content: "Written by" },
        { name: "twitter:data1", content: "Dyllon Schmehl" },
      ],
      link: [
        {
          hid: "canonical",
          rel: "canonical",
          href: `${this.$config.baseURL}/post/${this.$route.params.slug}`,
        },
      ],
    };
  },
};
</script>

<style lang="scss">
/* STYLING SPECIFIC TO BLOG POSTS GOES HERE */
.nuxt-content {
  h1 {
    font-weight: bold;
    font-size: 1.8rem;
    margin: 1rem 0;
    @media screen and (max-width: 768px) {
      font-size: 1.4rem;
    }
  }
  h2 {
    font-weight: bold;
    font-size: 1.6rem;
    margin: 1rem 0;
    @media screen and (max-width: 768px) {
      font-size: 1.3rem;
    }
  }
  h3 {
    font-weight: bold;
    font-size: 1.4rem;
    margin: 1rem 0;
    @media screen and (max-width: 768px) {
      font-size: 1.2rem;
    }
  }
  h4 {
    font-weight: bold;
    font-size: 1.2rem;
    margin: 0.75rem 0;
    @media screen and (max-width: 768px) {
      font-size: 1.1rem;
    }
  }

  p {
    margin-bottom: 1rem;
    font-size: 1.1rem;

    .nuxt-content p:last-child {
      margin-bottom: 0;
    }
  }

  li {
    list-style: inside !important;
  }

  // Give a padding to anything that follows an image, except another image
  .img + :not(.img) {
    margin-top: 1rem;
  }

  // And same for if the image follows anything that is not an image
  :not(.img) + .img {
    margin-top: 1rem;
  }
}
// Hover icon link
.icon.icon-link {
  width: 0;
}

.nuxt-content h1 > a::before,
.nuxt-content h2 > a::before,
.nuxt-content h3 > a::before,
.nuxt-content h4 > a::before {
  content: "#";
  display: block;
  float: left;
  margin-left: -1.25rem;
  color: $text;
  opacity: 0;
  font-weight: 400;
  font-size: 1.25rem;
  line-height: 1.75rem;
  line-height: 2rem;
  padding-right: 0.5rem;
  position: absolute;
}

.nuxt-content h2:hover > a::before,
.nuxt-content h3:hover > a::before {
  opacity: 1;
}

// Margin around code highlighting
.nuxt-content-highlight {
  margin: 1rem 0;
}

// Markdown tables, by default, apply Bulma table styling https://bulma.io/documentation/elements/table/
table {
  @extend .table;
  @extend .is-fullwidth;
  @extend .is-hoverable;
}
</style>
