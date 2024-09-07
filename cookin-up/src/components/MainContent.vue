<script lang="ts">
import Ingredients from './Ingredients.vue';
import List from './List.vue'
import ShowRecipe from './ShowRecipe.vue';

type Page = 'Ingredients' | 'ShowRecipe'

export default {
  data() {
    return {
      ingredientes: [] as string[],
      content: 'Ingredients' as Page
    }
  },
  components: { Ingredients, List, ShowRecipe },
  methods: {
    addIgredients(igrediente: string) {
      this.ingredientes.push(igrediente)
    },
    removeIngredients(ingrediente: string) {
      this.ingredientes = this.ingredientes.filter(iList => ingrediente !== iList)
    },
    nav(page: Page) {
      this.content = page
    }
  }
}

</script>

<template>
  <main class="conteudo-principal">
    <List :ingredientes="ingredientes" />
    <KeepAlive include="Ingredients">
      <Ingredients v-if="content == 'Ingredients'" @add-ingredient="addIgredients"
        @remove-ingredients="removeIngredients" @search-recipe="nav('ShowRecipe')" />
      <ShowRecipe v-else-if="content == 'ShowRecipe'" :ingredients="ingredientes" @search-recipe="nav('Ingredients')" />
    </KeepAlive>
  </main>
</template>

<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #FFFAF3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

.sua-lista-texto {
  color: var(--coral, #F0633C);
  display: block;
  text-align: center;
  margin-bottom: 1.5rem;
}

.ingredientes-sua-lista {
  display: flex;
  justify-content: center;
  gap: 1rem 1.5rem;
  flex-wrap: wrap;
}

.lista-vazia {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.25rem;

  color: var(--coral, #F0633C);
  text-align: center;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>