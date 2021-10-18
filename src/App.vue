<template>
  <div class="container">
    <div class="row">
      <h1>Mercado de monedas</h1>

      <tbody class="main__grid">
        <tr v-for="coin in filteredCoins" :key="coin.id" class="moneda">
          <div class="img">
            <img :src="coin.image" :alt="coin.name" class="me-2" />
          </div>
          <td class="nombres">
            <span class="nombre">
              {{ coin.name }}
            </span>
            <span class="text-muted text-uppercase nombre__corto">
              {{ coin.symbol }}
            </span>
          </td>

          <div class="precios">
            <td class="precio">{{ coin.current_price.toLocaleString() }}</td>
            <br>
            <td
              class="precio__variacion"
              :class="[
                coin.price_change_percentage_24h > 0
                  ? 'text-success'
                  : 'text-danger',
              ]"
            >
              {{ coin.price_change_percentage_24h }}
            </td>
          </div>
        </tr>
      </tbody>
    </div>
  </div>

  <footer class="footer">
    <p>Powered by 
      <a href="https://daviiduhh.com">daviiduhh</a>
    </p>
  </footer>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      coins: [],
      filteredCoins: [],
      titles: ["#", "Moneda", "Precio", "Variación"],
    };
  },
  async mounted() {
    const res = await fetch(
      "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=20&page=1&sparkline=false"
    );
    const data = await res.json();
    this.coins = data;
    this.filteredCoins = data;
  },
};
</script>

<style>
</style>
