<template>
  <div class="countries-list">
    <ul class="countries">
      <li v-for="country in fetchedData" :key="country.name" class="country">
        <img :src="country.flags.png" alt="Flag" class="country-flag">
        <div class="country-details">
          <h3 class="country-name">{{ country.name.common }}</h3>
          <p class="country-info">
            <span class="country-capital">{{ country.capital[0] }}</span>
            <span class="country-currency">{{ getFirstCurrency(country.currencies) }}</span>
          </p>
        </div>
      </li>
    </ul>
  </div>
  <button @click="loadCountries" class="load-button">Подгрузить страны</button>
</template>

<script>
import axios from 'axios'
export default {
  methods: {
    loadCountries() {
      axios
        .get("https://restcountries.com/v3.1/all")
        .then((response) => {
          console.log(response.data);
          this.fetchedData = response.data.slice(0, 10);
        })
        .catch((error) => {
          console.error(error);
        });
    },
    getFirstCurrency(currencies) {
      const currencyValues = Object.values(currencies);
      if (currencyValues.length > 0) {
        return currencyValues[0].name;
      }
      return '';
    }
  },
  data() {
    return {
      fetchedData: []
    };
  }, 
  name: "FetchCountries",
};
</script>

<style>
.countries-list {
  margin: 20px;
}

.countries {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px;
}

.country {
  background-color: #f0f0f0;
  border-radius: 5px;
  padding: 20px;
  display: flex;
  align-items: center;
}

.country-flag {
  width: 50px;
  height: auto;
  margin-right: 20px;
}

.country-details {
  flex-grow: 1;
}

.country-name {
  margin: 0;
  font-size: 18px;
  font-weight: bold;
}

.country-info {
  margin: 5px 0;
}

.country-capital {
  font-weight: bold;
}

.country-currency {
  margin-left: 10px;
  font-style: italic;
}

.load-button {
  padding: 12px 24px;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
  border-radius: 4px;
  background-color: #7298d5;
  color: #fff;
  border: none;
  cursor: pointer;
}
</style>
