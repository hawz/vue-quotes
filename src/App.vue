<template>
  <div class="container">
    <app-header :maxQuotes="maxQuotes" :quoteCount="quotes.length"></app-header>
    <app-new-quote @quoteAdded="newQuote"></app-new-quote>
    <app-quote-grid :quotes="quotes" @quoteDeleted="deleteQuote"></app-quote-grid>
    <div v-if="canInsertQuotes" class="text-center alert alert-info">
      <b>Info</b>: click on a quote to delete it.
    </div>
    <div v-else class="text-center alert alert-warning">
      <b>Warning</b>: Please delete some quotes before inserting a new one.
    </div>
  </div>
</template>

<script>
import QuoteGrid from "./components/QuoteGrid.vue";
import NewQuote from "./components/NewQuote.vue";
import Header from "./components/Header.vue";
export default {
  components: {
    appQuoteGrid: QuoteGrid,
    appNewQuote: NewQuote,
    appHeader: Header
  },
  data() {
    return {
      quotes: ["Just a quote to see something"],
      maxQuotes: 10
    };
  },
  methods: {
    newQuote(quote) {
      if (this.quotes.length < this.maxQuotes) {
        this.quotes.push(quote);
      }
    },
    deleteQuote(index) {
      this.quotes.splice(index, 1);
    }
  },
  computed: {
    canInsertQuotes() {
      return this.quotes.length < this.maxQuotes;
    }
  }
};
</script>

<style>
</style>
