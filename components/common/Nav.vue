<template>
  <nav class="nav">
    <ul class="nav__list">
      <li
        v-for="(item, index) in navItems"
        :key="index"
        class="nav__item"
        @click="close()"
      >
        <nuxt-link
          :to="`/${item.name}`"
          class="nav__link"
          :aria-label="`${item.name}ページに遷移する`"
          >{{ item.name }}</nuxt-link
        >
        <div class="nav__spacer" />
        <ul v-if="item.children" class="nav__dropdown">
          <li
            v-for="(children, childrenIndex) in item.children"
            :key="childrenIndex"
            class="nav__dropdownItem"
          >
            <nuxt-link
              :to="`/${item.name}/${children.path}`"
              class="nav__link -reverce"
              :aria-label="`${children.name}ページに遷移する`"
              >{{ children.name }}</nuxt-link
            >
          </li>
        </ul>
      </li>
    </ul>
  </nav>
</template>

<script>
import { mapMutations } from 'vuex'

export default {
  data() {
    return {
      navItems: [
        {
          name: 'research',
          children: [
            {
              name: 'ITS',
              path: 'its',
            },
            {
              name: 'Network',
              path: 'network-architecture',
            },
            {
              name: 'IoT',
              path: 'iot',
            },
          ],
        },
        { name: 'topics' },
        { name: 'advisor' },
        { name: 'education' },
        {
          name: 'publications',
          children: [
            {
              name: '2021年度',
              path: '2021',
            },
            {
              name: '2020年度',
              path: '2020',
            },
            {
              name: '2019年度',
              path: '2019',
            },
            {
              name: '2018年度',
              path: '2018',
            },
          ],
        },
        { name: 'members' },
        { name: 'contact' },
      ],
    }
  },
  methods: {
    ...mapMutations(['close']),
  },
}
</script>

<style lang="scss" scoped>
.nav {
  &__list {
    display: flex;
    height: 1.5em;

    @include mq(desk) {
      flex-direction: column;
      align-items: center;
      height: auto;
      color: #fff;

      a:hover {
        color: #dedede;
        transition: 0.3s;
      }
    }
  }

  &__spacer {
    height: 1.35rem;
  }

  &__dropdown {
    height: 0;
    overflow: hidden;
    font-size: 1rem;
    color: #fff;
    text-align: center;
    background-color: $main-color;
    border-radius: 0 0 12px 12px;
    transition: 0.2s;

    @include mq(desk) {
      display: none;
    }
  }

  &__dropdownItem {
    & + & {
      padding-top: 1rem;
    }
  }

  &__item {
    font-family: $font-set-en;
    font-size: 1.25rem;
    font-weight: 500;
    text-transform: capitalize;

    & + & {
      margin-left: 2.5rem;

      @include mq(desk) {
        margin-top: 1.5rem;
        margin-left: 0;
      }
    }

    &:hover .nav__dropdown {
      height: auto;
      padding: 1rem 0;
      transition: 0.3s;
    }
  }

  &__link {
    position: relative;
    display: inline-block;
    transition: 0.3s;

    &:hover {
      color: #666;
    }

    &:hover.-reverce {
      color: #ddd;
    }

    &::after {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 2px;
      content: '';
      background-color: $main-color;
      transition: 0.3s;

      @include mq(desk) {
        background-color: #fff;
      }
    }

    &:hover::after {
      width: 100%;
    }
  }
}
</style>
