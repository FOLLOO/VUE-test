<script>
  import PageHeader from "@/components/page-header/PageHeader.vue";
  import {defineComponent} from "vue";
  import Search from "@/components/ui/inputs/Search.vue";
  import Button from '@/components/ui/bttons/Button.vue'
  import Table from '@/components/tables/Table.vue'

  import sort from '@/assets/icons/sort.svg';
  import filter from '@/assets/icons/filter.svg';

  export default defineComponent({
    components: {Search, PageHeader, Button, Table},
    data() {
      return {
        sort,
        filter,
        searchText: ''
      };
    },
     methods: {
       handleSearchInput(text) {
         this.searchText = text;
         this.currentPage = 1;
       },
     }
  })

</script>

<template>
  <div class="about page">
    <PageHeader title="Учебные сессии">
      <template v-slot:search>
        <Search
            @SearchInputChanged="handleSearchInput"
            :text="searchText"
        />
      </template>
      <template v-slot:filter>
        <Button
            :disabled="true"
          :image="filter"
          type="foreground"
        />
      </template>
      <template v-slot:sort>
        <Button
            :disabled="true"
          :image="sort"
          type="foreground"
        />
      </template>
      <template v-slot:extra>
        <Button
            :disabled="true"
            text="Создать"
            type="default"
        />
      </template>
    </PageHeader>

    <Table
      :search="searchText"
    />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    width: 100%;
    min-height: 100vh;
    gap: 2rem;
    display: flex;
    flex-direction: column;
    background: var(--color-background);
  }
}
</style>
