<template>
  <main>
    <header class="header header--home">
      <div class="container container--narrow">
        <div class="home-header">
          <div class="home-header__image">
            <img src="/img/about-me-image.jpg" alt="An image of Traek Wells" />
          </div>
          <div class="home-header__content">
            <h1>
              Front-end Developer. UI Designer.
              <span class="underline">Good Person</span>.
            </h1>
            <p>
              What’s up? I’m Traek, and welcome to my partition of the internet
              when I share what I'm learning and show what I've built.
            </p>
            <nuxt-link to="/projects" class="button button--primary"
              >See My Work
            </nuxt-link>
          </div>
        </div>
      </div>
    </header>
    <div class="section">
      <div class="wave-white"></div>
      <div class="container container--narrow">
        <h2 class="text-center">Stuff I've Built</h2>
        <hr />
        <p class="lead">
          Stuff I've built through trial and error, a lot of breaks and just
          hoping that everything worked. Check out some of my smaller stuff here
          <a
            href="https://codepen.io/traekwells"
            target="_blank"
            rel="noreferrer noopener"
            >on CodePen</a
          >.
        </p>
        <div class="projects">
          <ProjectCard
            v-for="project in projects"
            :key="project.path"
            :project="project"
          />
        </div>
      </div>
    </div>
    <div class="section section--secondary">
      <div class="wave-yellow"></div>
      <div class="container container--narrow">
        <h2 class="text-center">Stuff I've Written</h2>
        <hr />
        <p class="lead mb-4">
          Sharing what I've learned in the hopes of solidify the knowledge and
          helping others however I can.
        </p>
        <div class="blogs">
          <BlogCard v-for="blog in blogs" :key="blog.path" :blog="blog" />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import ProjectCard from '@/components/ProjectCard'
import BlogCard from '@/components/BlogCard'
import getMetaData from '@/config/getMetaData.js'

export default {
  components: {
    ProjectCard,
    BlogCard,
  },
  async asyncData({ $content }) {
    const projects = await $content('projects')
      .where({ featured: true })
      .fetch()
    const blogs = await $content('blog').fetch()
    return { projects, blogs }
  },
  computed: {
    meta() {
      const metaData = {
        type: 'page',
        url: `https://traek.dev/`,
        title: 'UI Developer',
        description:
          "What’s up? I’m Traek, and welcome to my partition of the internet when I share what I'm learning and show what I've built.",
      }

      return getMetaData(metaData)
    },
  },
  head() {
    return {
      title: 'UI Developer',
      meta: [...this.meta],
      link: [
        {
          hid: 'canonical',
          rel: 'canonical',
          href: `https://traek.dev/`,
        },
      ],
    }
  },
}
</script>

<style lang="scss">
.home-header {
  display: flex;
  justify-content: center;

  @include respond-to(phone) {
    flex-direction: column;
    text-align: center;
  }

  h1 {
    font-weight: normal;
  }

  &__image {
    flex-basis: 35%;
    margin-right: 6rem;
    position: relative;
    z-index: 10;
    overflow: hidden;
    border-radius: 1rem;
    height: 40rem;
    margin-bottom: -7rem;

    @include respond-to(phone) {
      display: none;
    }

    @include respond-to(tab-port) {
      height: 35rem;
      margin-right: 5rem;
    }

    &::before {
      content: '';
      position: absolute;
      top: 0;
      bottom: 0;
      right: 0;
      left: 0;
      background-color: rgba(#561c6d, 0.55);
    }

    img {
      object-fit: cover;
      height: 100%;
    }
  }

  &__content {
    flex-basis: 50%;
    z-index: 10;

    p {
      font-size: 2rem;
    }

    @include respond-to(tab-port) {
      flex-basis: 70%;
    }
  }
}

.blogs {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 6rem 0;
}
</style>
