<template>
  <main class="home">
    <transition name="fade">
      <div v-if="!isLoading">
        <Introduction
          :name="pageData.name"
          :email="pageData.email"
          :intro="pageData.intro"
          :roles="pageData.roles"
          :tagline="pageData.tagline"
        />

        <About :technologies="pageData.technologies" />

        <Experience :experience="pageData.experience.data" />

        <Work :projects="pageData.projects.data" />

        <Contact />
      </div>
    </transition>

    <transition name="fade">
      <Loader v-if="isLoading" />
    </transition>
  </main>
</template>

<script>
import getData from '~/api/getData'

import Introduction from '~/views/Introduction'
import About from '~/views/About'
import Experience from '~/views/Experience'
import Work from '~/views/Work'
import Contact from '~/views/Contact'

import Loader from '~/components/Loader'

export default {
  components: {
    Introduction,
    About,
    Experience,
    Work,
    Contact,
    Loader,
  },
  data() {
    return {
      isLoading: true,
      pageData: {},
    }
  },
  watch: {
    isLoading() {
      if (!this.isLoading) {
        this.scrollToHash()
      }
    },
  },
  created() {
    getData('37jZbmQSggC4cQCNrjIXYI', this)
  },
  methods: {
    scrollToHash() {
      setTimeout(() => {
        const { hash } = this.$route

        if (hash) {
          document.querySelector(hash).scrollIntoView({
            behavior: 'smooth',
            block: 'start',
          })
        }
      })
    },
  },
}
</script>

<style lang="scss" scoped>
.home {
  min-height: 100vh;
  position: relative;
  padding-top: 90px;
  padding-bottom: $space-lg;
}

@media screen and (min-width: $bp-tablet) {
  .home {
    display: flex;
    flex-direction: column;
    padding: 120px $padding-lg;
    max-width: $site-width;
    margin: 0 auto;
  }
}
</style>
