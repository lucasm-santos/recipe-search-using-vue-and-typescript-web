<script lang="ts">
import type ICateogria from '@/interface/ICategoria';
import type { PropType } from 'vue';
import Tag from './Tag.vue';
import SelecIngredients from './SelecIngredients.vue';

export default {
    props: {
        categoria: { type: Object as PropType<ICateogria>, required: true }
    },
    components: { Tag, SelecIngredients },
    emits: ['addIngredient', 'removeIngredients']
}
</script>

<template>
    <article class="categoria">
        <header class="cateogira__cabecalho">
            <img :src="`/imagens/icones/categorias_ingredientes/${categoria.imagem}`" alt="" class="categoria__imagem">
            <h2 class="paragrafo-lg categoria__nome">{{ categoria.nome }}</h2>
        </header>
        <ul class="categoria__ingredientes">
            <li v-for="ingrediente in categoria.ingredientes" :key="ingrediente">
                <SelecIngredients :ingrediente="ingrediente" @add-ingredient="$emit('addIngredient', $event)"
                    @remove-ingredients="$emit('removeIngredients', $event)" />
            </li>
        </ul>
    </article>
</template>


<style scoped>
.categoria {
    width: 19.5rem;
    padding: 1rem;
    border-radius: 1rem;
    background: var(--branco, #FFF);
    box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
    height: 100%;

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
}

.categoria__cabecalho {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
}

.categoria__imagem {
    width: 3.5rem;
}

.categoria__nome {
    text-align: center;
    color: var(--verde-medio, #3D6D4A);
    font-weight: 700;
}

.categoria__ingredientes {
    display: flex;
    justify-content: center;
    gap: 0.5rem;
    flex-wrap: wrap;
}
</style>