<template>
  <section id="work" class="container">
    <SectionHeader text="My work" :index="3" />

    <RecentProjects :projects="projects" />

    <RecentPosts />
  </section>
</template>

<script>
import SectionHeader from '~/components/SectionHeader'
import RecentProjects from '~/components/RecentProjects'
import RecentPosts from '~/components/RecentPosts'

import getBlogPosts from '~/api/getBlogPosts'

export default {
  components: {
    SectionHeader,
    RecentProjects,
    RecentPosts,
  },
  props: {
    projects: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      isLoading: true,
      pageData: {},
    }
  },
  created() {
    getBlogPosts(6, this)
  },
}
</script>

<style lang="scss" scoped>
.container {
  font-family: 'Poppins';
  margin-top: 200px;
  padding-top: $space-xxl;
}

.more-projects {
  display: inline-block;
  background-color: transparent;
  color: $c-light-shades;
  border: 1px solid $c-light-shades;
  border-radius: 4px;
  font-size: 14px;
  text-decoration: none;
  margin: $space-xs 0;
  padding: $space-xs $space-sm;
}

.posts {
  display: flex;
  flex-wrap: wrap;

  &-header {
    margin-top: $space-xxl;
  }
}

.all-posts {
  display: inline-block;
  background-color: transparent;
  color: $c-light-shades;
  border: 1px solid $c-light-shades;
  border-radius: 4px;
  font-size: 14px;
  text-decoration: none;
  margin: $space-sm 0;
  padding: $space-xs $space-sm;
}

@media screen and (min-width: $bp-tablet) {
  .container {
    padding-top: $space-xxxl;
  }

  .more-projects {
    margin: 0;
    margin-right: $space-xs;
    transition: background-color ease 250ms 50ms, color ease 300ms;

    &:hover {
      background-color: $c-light-shades;
      color: $c-dark-shades;
    }
  }

  .all-posts {
    margin-right: $space-xs;
    transition: background-color ease 250ms 50ms, color ease 300ms;

    &:hover {
      background-color: $c-light-shades;
      color: $c-dark-shades;
    }
  }
}
</style>
