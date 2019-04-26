<template>
  <div class="container">
    <h1>{{ $t('default.' + (ammotype || 'ammo')) }}</h1>
    <my-table
      v-if="!error && ammoListings"
      v-bind:rows="ammoListings.items"
      :pages="ammoListings.pages"
      v-bind:ammotype="ammotype"
      v-bind:vendors="[null].concat(vendors.map(i => i.name))"
    ></my-table>
    <div v-if="error">ERROR {{ error }}</div>
    <div v-if="!ammoListings">{{ $t('default.loading') }}</div>
  </div>
</template>

<script lang="ts">
import MyTable from '~/components/my-table.vue'
import { getUrl } from '~/helpers'
import gql from 'graphql-tag'

export default {
  head() {
    const link: any[] = []
    const url = `https://ammobin.ca/${this.$i18n.locale !== 'en' ? this.$i18n.locale + '/' : ''}${this.ammotype ||
      'ammo'}`
    if (this.page > 1) {
      link.push({
        rel: 'prev',
        href: getUrl(url, this.page - 1, this.subtype),
      })
    }
    if (this.ammoListings && this.ammoListings.pages > this.page) {
      link.push({
        rel: 'next',
        href: getUrl(url, this.page + 1, this.subtype),
      })
    }
    return {
      title: (this.subtype || this.itemtype || 'Ammo') + ' Prices', //TODO: en francais
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `The place to view the best ${this.subtype || this.itemtype || 'ammo'} prices across ${this
            .province || 'Canada'}.`, //TODO: en francais
        },
      ],
      link,
    }
  },
  apollo: {
    vendors: {
      query: gql`
        query getVendors {
          vendors {
            name
          }
        }
      `,
    },
    ammoListings: {
      query: gql`
        query getAmmoListings(
          $itemtype: ItemType
          $page: Int
          $pageSize: Int
          $subtype: String
          $province: Province
          $vendor: String
          $query: String
          $sortField: SortField
          $sortOrder: SortOrder
        ) {
          ammoListings(
            itemType: $itemtype
            page: $page
            pageSize: $pageSize
            subType: $subtype
            province: $province
            vendor: $vendor
            sortField: $sortField
            query: $query
            sortOrder: $sortOrder
          ) {
            pages
            items {
              name
              brand
              subType
              minPrice
              maxPrice
              minUnitCost
              maxUnitCost
              img
              vendors {
                name
                price
                link
                unitCost
                vendor
              }
            }
          }
        }
      `,
      variables() {
        // Use vue reactive properties here
        return {
          page: this.page,
          subType: this.subtype || null,
          pageSize: this.pageSize,
          itemtype: this.itemtype || null,
          province: this.province || null,
          vendor: this.vendor || null,
          query: this.query || null,
          sortField: this.sortField || null,
          sortOrder: this.sortOrder || null,
        }
      },
      prefetch: ({ route }) => {
        let itemType = route.params.itemtype || route.query.itemtype || null
        // todo: fix this
        if (false && ['rimfire', 'centerfire', 'shotgun'].indexOf(itemType) === -1) {
          return false // hard 404
        }

        return {
          page: Number(route.query.page) || 1,
          subtype: route.query.subtype || null,
          pageSize: Number(route.query.pageSize) || 25,
          province: route.query.province || null,
          itemType,
          vendor: route.query.vendor || null,
          query: route.query.query || null,
          sortField: route.query.sortField || null,
          sorderOrder: route.query.sortOrder || null,
        }
      },
      watchLoading(isLoading /*, countModifier*/) {
        if (this.$nuxt && this.$nuxt.$loading && this.$nuxt.$loading.start) {
          if (isLoading) {
            this.$nuxt.$loading.start()
          } else {
            this.$nuxt.$loading.finish()
          }
        } else {
          console.log('no loading start/finish')
        }
      },
    },
  },
  data() {
    return {
      error: null,
      ammoListing: null,
    }
  },
  computed: {
    page() {
      return Number(this.$route.query.page) || 1
    },
    subtype() {
      return this.$route.query.subtype || null
    },
    province() {
      return this.$route.query.province || null
    },
    pageSize() {
      return Number(this.$route.query.pageSize) || 25
    },
    itemtype() {
      let ammoType = this.$route.params.itemtype || this.$route.query.itemtype || null
      return ammoType
    },
    vendor() {
      return this.$route.query.vendor || null
    },
    query() {
      return this.$route.query.query || null
    },
    sortOrder() {
      return this.$route.query.sortOrder || null
    },
    sortField() {
      return this.$route.query.sortField || null
    },
  },
  components: {
    MyTable,
  },
  validate({ params }) {
    // todo: use proper const here
    return true || [null, 'rimfire', 'centerfire', 'shotgun'].indexOf(params.ammotype) >= 0
  },
}
</script>
