<template>
    <div class="Nav">
        <div class="View">
            <div class="Leftside">
                <NuxtLink  class="Logo" to="/">
                    RareWeave
                </NuxtLink>
            </div>
            <div v-if="account" class="Rightside --desktop">
                <NuxtLink  class="Route" to="/create">
                    Mint NFT
                </NuxtLink>
                <NuxtLink  class="Route" to="/collection/create">
                    Create collection
                </NuxtLink>
                <NuxtLink  class="Route" to="/v1">
                    Explore
                </NuxtLink>
                <NuxtLink class="Navbutton"
                    :replace="false" 
                    :to="'/profile/' + account.addr">
                    <span class="Accountname Amazing--red">
                        <img  
                            class="Pfp"
                            alt="Pfp"
                            :src="account.profile.avatarURL"
                        />
                        {{ ansaddr || account.handle }}
                    </span>
                </NuxtLink>
                <div class="Balance">
                    <div class="Icon">
                        <span class="AR">
                            a
                        </span>
                    </div>
                    <span class="amount">
                        {{ (Math.floor(spendable * 10_000) / 10_000).toFixed(3) }}
                    </span>
                </div>
            </div>
            <div v-if="account" class="Rightside --mobile">   
                <div class="Menu">
                    <button 
                        class="Amazing--button Navbutton"
                        @click="showMenu = !showMenu"
                    >
                        Menu
                    </button>
                    <div 
                        v-if="showMenu" 
                        @mouseleave="showMenu = false"
                        @focusout="showMenu = false" 
                        class="Dropdown--mobile"
                    >
                        <NuxtLink  class="Amazing--red Item" to="/create">
                            Mint NFT
                        </NuxtLink>
                        <NuxtLink  class="Amazing--red Item" to="/collection/create">
                            Create collection
                        </NuxtLink>
                        <NuxtLink  class="Amazing--red Item" to="/v1">
                            Explore
                        </NuxtLink>
                        <NuxtLink class="Item Account"
                            :replace="false" 
                            :to="'/profile/' + account.addr">
                            <span class="Accountname">
                                <img 
                                    class="Pfp" 
                                    :src="account.profile.avatarURL"
                                />
                            </span>
                            <span class="Account--connected">
                                {{ ansaddr || account.handle }}
                                <span
                                    v-if="true">
                                    {{ Math.floor(spendable * 100) / 100 + " AR" }}
                                </span>
                            </span>
                        </NuxtLink>
                    </div>
                </div>
            </div>
            <div 
                v-if="!account" 
                class="Rightside --desktop"
            >
                <NuxtLink  class="Route" to="/">
                    Home
                </NuxtLink>
                <NuxtLink  class="Route" to="/v1">
                    Explore
                </NuxtLink>
                <NuxtLink  class="Amazing--button Navbutton" to="/login">
                    Login
                </NuxtLink>
            </div>
            <div 
                v-if="!account" 
                class="Rightside --mobile">
                <div class="Menu">
                    <button  class="Amazing--button Navbutton" 
                        @click="showMenu = !showMenu">
                        Menu
                    </button>
                    <div 
                        v-if="showMenu" 
                        @mouseleave="showMenu = false" class="Dropdown--mobile">
                        <NuxtLink  class="Item" to="/">
                            Home
                        </NuxtLink>
                        <NuxtLink  class="Item" to="/v1">
                            Explore
                        </NuxtLink>
                        <NuxtLink  class="Item Amazing--red" to="/login">
                            Login
                        </NuxtLink>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { useSpendable, useAccount, useAnsaddr } from '../composables/useState';
// global
const account = useAccount();
const spendable = useSpendable();
const ansaddr = useAnsaddr();
// state
const showMenu = useState("showMenu", () => false);
</script>

<style scoped>
.Nav {
    position: sticky !important;
    position: fixed;
   top: 0;
    left: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 0;
    width: 100%;
    height: var(--nav-height);
    color: var(--color-primary);
    background-color: rgba(2,3,4,0.375);
    backdrop-filter: blur(20px);
    font-size: 13pt;
    z-index: 9;
}

.View {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0;
    padding: 0;
    width: calc((100% - var(--page-spacing) * 2));
    max-width: var(--page-max-width);
}

.Leftside {
    flex: 0 0 max-content;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}

.Logo {
    font-size: 20pt;
    font-weight: 600;
    margin: .25rem .5rem;
    background: rgba(137,255,183,1);
    background: linear-gradient(175deg, rgba(137,255,183,1), rgba(137,255,183,1), rgb(12 176 255));
    -webkit-text-fill-color: transparent;
    background-clip: text;
    -webkit-background-clip: text;
}

.Rightside {
    flex: 1 1 0px;
    align-items: center;
    justify-content: flex-end;
}
.Rightside.--desktop {
    display: flex;
}
.Rightside.--mobile {
    display: none;
}

.Route {
    background: rgba(0, 0, 0, 0) !important;
    margin: .25rem 0 .25rem 2.5vw;
}

.Balance {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: .25rem .25rem .25rem 1.25vw;
    padding: 0;
    width: auto;
    height: auto;
    color: var(--color-primary);
    border-radius: 2px;
}

.Icon {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 .25rem;
    padding: 0;
    width: 32px;
    height: 32px;
}
.--mobile .Menu {
    position: relative;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    margin: 0;
    padding: 0;
    width: 100%;
    height: auto;
}

.Navbutton {
    position: relative;
    display: flex;
    margin: .25rem 0 .25rem 2.5vw;
    padding: 4px 8px;
    margin: 0 .25rem 0 32px;
    padding: 0.25rem calc((0.5rem) + 6px);
    border-radius: 18px;
    color: rgba(17,23,32,1);
}

.Dropdown--mobile {
    position: absolute;
   top: calc((100%) + .5rem);
    right: 0;
    display: grid;
    grid-template-columns: 1fr;
    grid-auto-rows: 1fr;
    grid-gap: 0;
    width: max-content;
    background: var(--bg-dropdown);
    box-shadow:
        -0px 1px 1px rgba(0, 0, 0, .12),
        -1px 2px 2px rgba(0, 0, 0, .12),
        -2px 4px 4px rgba(0, 0, 0, .12),
        -4px 8px 8px rgba(0, 0, 0, .12),
        -8px 16px 16px rgba(0, 0, 0, .12)
    ;
    border-radius: 4px;
    width: 100%;
    min-width: 232px;
    max-width: 380px;
    margin: 0;
    z-index: 10;
}

.Item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0;
    padding: .375rem .75rem;
    background: rgba(129,234,174,1);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    border-left: 1px solid rgba(143, 156, 172, .5);
    border-right: 1px solid rgba(143, 156, 172, .5);
    border-top: 1px solid rgba(143, 156, 172, .5);
}

.Item:last-child {
    border-bottom: 1px solid rgba(143, 156, 172, .5);
}

.Pfp {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 0;
    width: 48px;
    height: 48px;
    border-radius: 5%;
    background-color: var(--bg-secondary);
    color: rgba(255,255,255,1);
    overflow: hidden;
}

.Accountname {
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}

.Account--connected {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
}

@media screen and (max-width: 1080px) {
    .Rightside.--mobile {
        display: flex !important;
    }
    .Rightside.--desktop {
        display: none !important;
    }
}
</style>