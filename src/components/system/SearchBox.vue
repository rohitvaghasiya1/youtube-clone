<template>
  <div class="YL__toolbar-input-container header-search-bar row no-wrap">
    <div class="col">
      <q-input
        rounded
        outlined
        v-model="search"
        placeholder="Search"
        @focus="showSearchIcon = true"
        @blur="showSearchIcon = false"
        class="col"
      >
        <template v-if="showSearchIcon" v-slot:prepend>
          <q-icon name="search" />
        </template>
        <template v-slot:append>
          <q-icon name="keyboard" class="q-mr-md" />
          <q-btn flat color="grey-3" text-color="grey-8" icon="search" />
        </template>
      </q-input>
    </div>
    <div class="col-1 text-right">
      <q-btn flat round color="grey-3" icon="mic" text-color="grey-8" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
defineOptions({
  name: "SearchBox",
});

const search = ref("");
const showSearchIcon = ref(false);

const props = defineProps({
  video: {
    type: Object,
    required: true,
  },
});
</script>
<style lang="scss">
.header-search-bar {
  max-width: 732px;
  margin: auto;
  width: 100%;
  @media screen and (max-width: 1439px) {
    max-width: 600px;
  }
  .q-field__control {
    height: 40px;
    padding-right: 0;
    .q-field__native {
      padding: 0;
    }
    .q-field__marginal {
      height: 40px;
      .q-btn-item {
        border-left: 1px solid rgba(0, 0, 0, 0.24);
        width: 68px;
        border-radius: 0 50px 50px 0;
        height: 40px;
      }
    }
  }
}
</style>
