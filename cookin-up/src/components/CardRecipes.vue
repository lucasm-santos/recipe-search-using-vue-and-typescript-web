<script lang="ts">
import type IRecipe from '@/interface/IRecipe';
import type { PropType } from 'vue';

export default {
    props: {
        recipe: { type: Object as PropType<IRecipe>, required: true }
    }
}
</script>

<template>
    <article class="categoria">
        <header class="cateogira__cabecalho">
            <img :src="`/imagens/receitas/${recipe.imagem}`" alt="" class="categoria__imagem">
            <h2 class="paragrafo-lg categoria__nome">{{ recipe.nome }}</h2>
        </header>
    </article>
</template>

<style scoped>
.categoria {
    width: 20rem;
    border-radius: 1rem;
    background: var(--branco, #FFF);
    box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);

    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 2rem;
}

.cateogira__cabecalho {
    display: flex;
    align-items: center;
    flex-direction: column;
}

.categoria__nome {
    padding: 2rem;
}

.categoria__imagem {
    width: 20rem;
    border-top-left-radius: 1rem;
    border-top-right-radius: 1rem;
}
</style>