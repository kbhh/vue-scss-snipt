
<template>
  <v-container>
    <v-row justify="space-between" class="market-place-detail-header">
      <v-col cols="12" md="5" class="mx-5">
        <span class="title">Gargle Marketplaces</span>
      </v-col>
      <v-col cols="12" md="2">
        <v-btn
          text
          color="primary"
          @click="
            $router.push({
              name: 'Requested Marketplaces'
            })
          "
        >Requested(0)</v-btn>
      </v-col>
    </v-row>
    <v-row class="mt-2 mx-5 mt-6">
      <div class="title">I want to</div>
      <div class="mx-2">
        <v-menu key="text" offset-y>
          <template v-slot:activator="{ attrs, on }">
            <v-btn text class="primary--text title" v-bind="attrs" v-on="on">
              {{ currentFilter }}
              <v-icon>mdi-menu-down</v-icon>
            </v-btn>
          </template>
          <v-list>
            <v-list-item
              color="primary"
              v-for="(item, i) in filters"
              :key="i"
              @click="currentFilter = item"
              link
            >
              <v-list-item-title v-text="item"></v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </div>
    </v-row>
    <v-row class="mt-5 mx-5">
      <p>Request a demo to find out what a product can do for your practice.</p>
    </v-row>
    <v-row class="my-6 mx-2">
      <v-col cols="12" md="4" v-for="(product, i) in filterdProducts" :key="i">
        <MarketCard
          :id="product.id"
          :title="product.Product"
          :previewText="product['Preview Summary']"
          :logo="`${$websiteAssetUrl}/partners/${product.logo}`"
          :primaryColor="product.color"
        ></MarketCard>
      </v-col>
    </v-row>
    <v-row class="my-6 mx-5">
      <div class="title">Shop all Gargle products</div>
    </v-row>
    <v-row class="mx-2">
      <v-col cols="12" md="4" class="my-2" v-for="(product, i) in products" :key="i">
        <MarketCard
          :id="product.id"
          :title="product.Product"
          :previewText="product['Preview Summary']"
          :logo="`${$websiteAssetUrl}/partners/${product.logo}`"
          :primaryColor="product.color"
        ></MarketCard>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import MarketCard from '@/components/Cards/MarketCard'
export default {
  computed: {
    filterdProducts() {
      return this.products.filter((product) => {
        return product.categories.includes(this.currentFilter)
      })
    },
    products() {
      return this.$store.state.marketPlaces
    }
  },
  data() {
    return {
      currentFilter: 'Acquire New Patients',
      filters: [
        'Improve Patient Engagement',
        'Acquire New Patients',
        'Build Brand Awareness'
      ]
    }
  },
  components: {
    MarketCard
  }
}
</script>
