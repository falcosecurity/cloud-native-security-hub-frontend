<template>
  <div>
    <Header hero />
    <b-container class="content">
      <b-row>
        <b-col sm="12" md="3" class="filter-panel">
          <section class="filter-group categories">
            <h3 class="title">
              Categories
            </h3>
            <b-btn-group vertical tag="ul" class="filters w-100">
              <b-btn
                v-for="category in categories"
                :key="category"
                tag="li"
                variant="light"
                class="text-left text-capitalize filter"
                :pressed="isSelectedCategory(category)"
                @click="toggleCategory(category)"
              >
                {{ category }}
              </b-btn>
            </b-btn-group>
          </section>
        </b-col>
        <b-col sm="12" md="9" tag="section" class="components">
          <transition-group name="zoom" tag="b-row" appear>
            <b-col
              v-for="component in components"
              :key="component.id"
              xs="12"
              sm="6"
              md="6"
              lg="4"
              xl="3"
            >
              <ComponentCard :component="component" />
            </b-col>
          </transition-group>
        </b-col>
      </b-row>
    </b-container>
    <Footer />
  </div>
</template>

<script>
import { mapState, mapGetters, mapActions } from 'vuex'
import Header from '@/components/Header'
import Footer from '@/components/Footer'
import ComponentCard from '@/components/ComponentCard'

export default {
  components: {
    Header,
    Footer,
    ComponentCard
  },
  computed: {
    ...mapState({
      vendors: state => state.vendors
    }),
    ...mapGetters(['categories', 'components', 'isSelectedCategory'])
  },
  methods: {
    ...mapActions(['toggleCategory'])
  }
}
</script>

<style scoped lang="scss">
  .content {
    min-height: calc(100vh - 140px - 228.8px - 32px); // 100 - footer - header - headerMargin
    margin-top: 2rem;
    margin-bottom: 2rem;
  }
  .title {
    text-align: center;
    width: 100%;
    margin-top: 0.5rem;
    font-size: 0.8rem;
  }
  .filter-panel {
    .filter-group {
      .filters {
        list-style-type: none;
        margin: 0;
        padding: 0;
        .filter {
          cursor: pointer;
          &:focus {
            box-shadow: 0 0 0 1px rgba(216, 217, 219, 0.5)
          }
        }
      }
      .title {
        margin: 1rem 0 0.3rem 0;
        font-family: Roboto;
        font-size: 1rem;
      }
    }
  }
</style>
