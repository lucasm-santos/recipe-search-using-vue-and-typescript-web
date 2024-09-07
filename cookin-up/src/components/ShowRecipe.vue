<script lang="ts">
import Button from './Button.vue';
import { GetRecipes } from '@/http/index';
import CardRecipes from './CardRecipes.vue';
import type IRecipe from '@/interface/IRecipe';
import type { PropType } from 'vue';
import { equalList } from '@/operations/list';


export default {
    props: {
        ingredients: { type: Array as PropType<String[]>, required: true },
    },
    data() {
        return { GettedRecipes: [] as IRecipe[] }
    },
    async created() {
        const recipes = await GetRecipes();

        this.GettedRecipes = recipes.filter((recipe) => {
            const canDoRecipe = equalList(recipe.ingredientes, this.ingredients);

            return canDoRecipe
        })
    },
    components: { CardRecipes, Button }
}
</script>

<!-- <template>
    <ul class="wrapper">
        <li v-for="categoria in categorias" :key="categoria.nome">
            <CardRecipes :categoria="categoria" />
        </li>
    </ul>
    <Button texto="Editar lista" @click="$emit('searchRecipe')" />
</template> -->

<template>
    <section class="mostrar-receitas">
        <h1 class="cabecalho titulo-receitas">Receitas</h1>

        <p class="paragrafo-lg resultados-encontrados">
            Resultados encontrados: {{ GettedRecipes.length }}
        </p>

        <div v-if="GettedRecipes.length" class="receitas-wrapper">
            <p class="paragrafo-lg informacoes">
                Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!
            </p>

            <ul class="receitas">
                <li v-for="recipes of GettedRecipes" :key="recipes.nome">
                    <CardRecipes :recipe="recipes" />
                </li>
            </ul>
        </div>

        <div v-else class="receitas-nao-encontradas">
            <p class="paragrafo-lg receitas-nao-encontradas__info">
                Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?
            </p>

            <img src="../assets/imagens/sem-receitas.png"
                alt="Desenho de um ovo quebrado. A gema tem um rosto com uma expressão triste.">
        </div>

        <Button texto="Editar lista" @click="$emit('searchRecipe')" />
    </section>
</template>



<style scoped>
.mostrar-receitas {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.titulo-receitas {
    color: var(--verde-medio, #3D6D4A);
    margin-bottom: 1.5rem;
}

.resultados-encontrados {
    color: var(--verde-medio, #3D6D4A);
    margin-bottom: 0.5rem;
}

.receitas-wrapper {
    margin-bottom: 3.5rem;
}

.informacoes {
    margin-bottom: 2rem;
}

.receitas {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}

.receitas-nao-encontradas {
    margin-bottom: 2rem;
}

.receitas-nao-encontradas__info {
    margin-bottom: 0.5rem;
}

@media only screen and (max-width: 767px) {
    .receitas-wrapper {
        margin-bottom: 2rem;
    }
}
</style>