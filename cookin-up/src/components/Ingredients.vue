<script lang="ts">
import { ObterCategorias } from '@/http/index';
import type ICateogria from '@/interface/ICategoria';
import CardCategory from './CardCategory.vue';
import Button from './Button.vue';

export default {
  name: 'Ingredients',
  data() {
    return {
      categorias: [] as ICateogria[]
    }
  },
  async created() {
    this.categorias = await ObterCategorias();
  },
  components: { CardCategory, Button },
  emits: ['addIngredient', 'removeIngredients', 'searchRecipe']
}

</script>
<template>
  <section class="selecionar-ingredientes">
    <h1 class="cabecalho titulo-ingredientes">Ingredientes</h1>

    <p class="paragrafo-lg instrucoes">
      Selecione abaixo os ingredientes da sua receita:
    </p>

    <ul class="categorias">
      <li v-for="categoria in categorias" :key="categoria.nome">
        <CardCategory :categoria="categoria" @add-ingredient="$emit('addIngredient', $event)"
          @remove-ingredients="$emit('removeIngredients', $event)" />
      </li>
    </ul>
    <p class="paragrafo dica">
      *Atenção: Consideramos que voce tem em casa sal, pimenta e agua.
    </p>
    <Button texto="Buscar receitas!" @click="$emit('searchRecipe')" />
  </section>
</template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}
</style>