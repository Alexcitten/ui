<template>
  <div class="Component">
    <NuxtLink 
      :to="'/nft/' + nft.contractTxId"
      class="Link"
    >
      <Graphic 
        :nft="nft"
      />
      <div class="Info">
        <label class="title">
          Name:
        </label>
        <span class="title">
          {{ nft.state.name }}
        </span>

        <label class="description">
          Description:
        </label>
        <span class="description">
          {{ nft.state.description }}
        </span>

        <label class="owner">
          Owner:
        </label>
        <span class="owner">
          {{ nft.owner.ansName || nft.owner.address }}
        </span>
        
        <label class="minter">
          Minter:
        </label>
        <span class="minter">
          {{ nft.state.minter }}
        </span>

        <label class="forsale">
          For Sale:
        </label>
        <span class="forsale">
          {{ nft.state.forSale ? "Yes" : "No" }}
        </span>

        <label class="price">
          {{ nft.state.listingDenom || "AR" }}
        </label>
        <span class="price">
          {{ nft.state.price > 0 ? (nft.state.price / 1e12).toFixed(2)+" ("+(nft.state.price)+" winston)" : "free" }}
        </span>

        <label class="royalty">
          Royalty:
        </label>
        <span class="royalty">
          {{ nft.state.royalty }} %
        </span>
        
        <label class="reservationBlockheight">
          Reservation bh:
        </label>
        <span class="reservationBlockheight">
          {{ nft.state.reservationBlockheight }}
        </span>
      </div>
    </NuxtLink>
  </div>
</template>
<script setup>
import Graphic from "./Graphic.vue";
const { nft } = defineProps([
  "nft"
]);
</script>
<style scoped>
.Component {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: flex-start;
  background: rgba(17,23,32,.5);
  width: 100%;
}

.Link {
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  width: 100%;
  height: 100%;
  border-bottom: 1px solid rgba(172, 172, 172, 0.5);
  border-left: 1px solid rgba(172, 172, 172, 0.5);
  padding: 1rem;
}

.Imagewrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  width: 316px;
  aspect-ratio: 1/1;
  
}

.Info {
  display: grid;
  grid-template-columns: 186px 1fr;
  width: 100%;
  height: calc((100%) - 1rem * 2);
  margin: 1rem 0;
  padding: 0 1rem;
}
</style>