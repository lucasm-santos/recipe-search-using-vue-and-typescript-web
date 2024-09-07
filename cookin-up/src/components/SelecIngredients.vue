<script lang="ts">
import Tag from './Tag.vue';

export default {
    components: { Tag },
    props: {
        ingrediente: { type: String, required: true }
    },
    data() {
        return {
            selected: false
        }
    },
    methods: {
        OnClick() {
            this.selected = !this.selected

            if (this.selected) {
                this.$emit('addIngredient', this.ingrediente)
            } else {
                this.$emit('removeIngredients', this.ingrediente);
            }
        }
    },
    emits: ['addIngredient', 'removeIngredients']
}
</script>

<template>
    <button class="ingrediente" @click="OnClick">
        <Tag :texto="ingrediente" :ativa="selected" />
    </button>
</template>

<style scoped>
.ingrediente {
    cursor: pointer;
}

.tag:hover {
    color: #78ba8a;
}
</style>