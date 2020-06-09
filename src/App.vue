<template>
  <div>
    <header class="header">
      <h1 class="header-title"><a href="/">AWS-ja-doc search</a></h1>
      <p class="header-subtitle">
        using
        <a href="https://github.com/algolia/vue-instantsearch">
          Vue InstantSearch
        </a>
      </p>
    </header>

    <div class="container">
      <ais-instant-search
        :search-client="searchClient"
        index-name="aws_ja_docs"
      >
        <div class="search-panel">
          <div class="search-panel__filters">
            <ais-refinement-list attribute="service" searchable />
            <ais-refinement-list attribute="doc" searchable />
            <ais-clear-refinements />

          </div>

          <div class="search-panel__results">
            <ais-search-box placeholder="Search here…" class="searchbox" />
            <ais-hits>
              <template slot="item" slot-scope="{ item }">
                <p class="ais-hits-service-name">{{ item.doc }} : <a :href="item.url" class="ais-hits-doc-link"> {{ item.title }}</a></p>
                <p><ais-highlight :hit="item" attribute="text" /></p>
              </template>
            </ais-hits>

            <div class="pagination"><ais-pagination /></div>
          </div>
        </div>
      </ais-instant-search>
    </div>
  </div>
</template>

<script>
import algoliasearch from 'algoliasearch/lite';
import 'instantsearch.css/themes/algolia-min.css';

export default {
  data() {
    return {
      searchClient: algoliasearch(
        'RVAICUX7HD',
        'd51653b9486bec74e5da8d1596b86eaa'
      ),
    };
  },
};
</script>

<style>
body,
h1 {
  margin: 0;
  padding: 0;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica,
    Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
}

.header {
  display: flex;
  align-items: center;
  min-height: 50px;
  padding: 0.5rem 1rem;
  background-image: linear-gradient(to right, #4dba87, #2f9088);
  color: #fff;
  margin-bottom: 1rem;
}

.header a {
  color: #fff;
  text-decoration: none;
}

.header-title {
  font-size: 1.2rem;
  font-weight: normal;
}

.header-title::after {
  content: ' ▸ ';
  padding: 0 0.5rem;
}

.header-subtitle {
  font-size: 1.2rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem;
}

.search-panel {
  display: flex;
}

.search-panel__filters {
  flex: 1;
  margin-right: 1em;
}

.search-panel__results {
  flex: 3;
}

.searchbox {
  margin-bottom: 2rem;
}

.pagination {
  margin: 2rem auto;
  text-align: center;
}

.ais-Hits-item {
  width: 100%;
}

.ais-hits-service-name {
  font-size: 0.8rem;
  padding: .1rem .4rem;
  font-size: .8rem;
  color: #3a4570;
  background-color: #dfe2ee;
  border-radius: 4px;
  width: auto;
}

.ais-hits-doc-link {
  font-size: 0.8rem;
}

.ais-RefinementList {
  margin-bottom: 1rem;
}

</style>
