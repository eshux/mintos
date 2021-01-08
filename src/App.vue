<template>
  <section class="section">
    <div class="container container-fluid">
      <div class="row center-xs">
        <div class="col-xs-12">
          <div class="wrapper">
            <div class="box-wrap box-wrap--upper">
               <BoxSelected
                v-for="{id, name} in selectedCurr"
                :key="id"
                :currency="name"
                @onClick="changeSelect(id)"
              />
            </div>
            <div class="box-wrap">
              <Box
                v-for="{id, name, select} in currencies"
                :key="id"
                :checkboxValue="select"
                :currency="name"
                @click="changeSelect(id)"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
/* eslint-disable no-param-reassign */
import { defineComponent } from 'vue';
import { currencyData, CurrencyData } from './data/currencyData';
import Box from './components/Box/Box.vue';
import BoxSelected from './components/BoxSelected/BoxSelected.vue';

const App = defineComponent({
  data() {
    return {
      currencies: currencyData,
    };
  },

  components: {
    Box,
    BoxSelected,
  },

  methods: {
    changeSelect(id: number) {
      return this.currencies.map((item) => {
        if (item.id === id) {
          item.select = !item.select;
        }
        return item;
      });
    },
  },

  computed: {
    selectedCurr(): CurrencyData[] {
      return this.currencies.filter((item) => item.select === true);
    },
  },
});

export default App;
</script>

<style src="./app.scss" lang="scss"></style>
