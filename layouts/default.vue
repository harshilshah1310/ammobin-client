<template>
  <div class="main">
    <a class="fork-me-hard-dady" href="https://github.com/ammobindotca" target="_blank" rel="noopener">
      <img
        style="position: absolute; top: 0; right: 0; border: 0;"
        src="~/assets/fork.png"
        alt="Fork me on GitHub"
        title="Fork me on GitHub"
      />
    </a>
    <div class="pure-menu pure-menu-horizontal pure-menu-scrollable light-grey">
      <ul class="pure-menu-list">
        <li class="pure-menu-item">
          <nuxt-link class="pure-menu-link" :class="{ 'pure-menu-selected': currentPage === '/' }" :to="path('/')"
            >AMMOBIN.CA</nuxt-link
          >
        </li>
        <li class="pure-menu-item">
          <nuxt-link
            class="pure-menu-link"
            :class="{ 'pure-menu-selected': currentPage === '/centerfire' }"
            :to="path('/centerfire')"
            >{{ $t('default.centerfire') }}</nuxt-link
          >
        </li>
        <li class="pure-menu-item">
          <nuxt-link
            class="pure-menu-link"
            :class="{ 'pure-menu-selected': currentPage === '/shotgun' }"
            :to="path('/shotgun')"
            >{{ $t('default.shotgun') }}</nuxt-link
          >
        </li>
        <li class="pure-menu-item">
          <nuxt-link
            class="pure-menu-link"
            :class="{ 'pure-menu-selected': currentPage === '/rimfire' }"
            :to="path('/rimfire')"
            >{{ $t('default.rimfire') }}</nuxt-link
          >
        </li>
        <li class="pure-menu-item">
          <nuxt-link
            class="pure-menu-link"
            :class="{ 'pure-menu-selected': currentPage === '/about' }"
            :to="path('/about')"
            >{{ $t('default.about') }}</nuxt-link
          >
        </li>
        <li class="pure-menu-item">
          <nuxt-link
            class="pure-menu-link"
            v-if="$i18n.locale === 'en'"
            :to="`/fr` + $route.fullPath"
            active-class="none"
            exact
          >
            {{ $t('links.french') }}
          </nuxt-link>
          <nuxt-link
            class="pure-menu-link"
            v-else
            :to="$route.fullPath.replace(/^\/[^\/]+/, '')"
            active-class="none"
            exact
          >
            {{ $t('links.english') }}
          </nuxt-link>
        </li>
      </ul>
    </div>
    <nuxt />
    <footer class="footer">
      AmmoBin.ca {{ new Date().getFullYear() }}
      <a v-bind:href="mail">Contact</a>
      <div>
        <a href="https://github.com/ammobindotca" target="_blank" rel="noopener">github</a> |
        <a href="https://www.instagram.com/ammobin.ca" target="_blank" rel="noopener">instagram</a> |
        <a href="https://status.ammobin.ca/" target="_blank" rel="noopener">status</a>
      </div>
    </footer>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component({
  head() {
    return {
      title: 'AmmoBin.ca',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.$t('home.tagline'),
        },
      ],
      htmlAttrs: {
        lang: this.$i18n.locale || 'en',
      },
      __dangerouslyDisableSanitizers: ['script'],
      script: [
        {
          innerHTML: JSON.stringify({
            '@context': 'http://schema.org',
            '@type': 'Person',
            name: 'Ammobin.ca',
            url: 'https://ammobin.ca',
            sameAs: ['https://github.com/ammobindotca', 'https://www.instagram.com/ammobin.ca'],
          }),
          type: 'application/ld+json',
        },
      ],
    }
  },
} as any)
export default class Layout extends Vue {
  // todo: attach correct types
  $router: any
  $i18n: any

  get currentPage() {
    return this.$router.path
  }

  mail = 'mailto:' + 'contact' + '@' + 'ammobin.ca' // this probably will do nothing to stop bots...

  path(url) {
    return this.$i18n.locale === 'en' ? url : '/' + this.$i18n.locale + url
  }
}
</script>

<style>
.footer {
  text-align: center;
  margin-top: 100px;
}

.light-grey {
  background-color: #f1f1f1;
}

/* hide fork me link on mobile*/

@media screen and (max-width: 35.5em) {
  .fork-me-hard-dady {
    display: none;
  }
}
</style>
