<template>
        <button class="button" @click="handleClick" :disabled="isDisabled">
            <span class="icon">
                <i :class="icon"></i>
            </span>
            <span>{{texto}}</span>
        </button>
</template>

<script lang="ts">
import {defineComponent} from 'vue'

export default defineComponent({
    name: 'ButtonForm',
    props:{
        texto: {type: String},
        icon: {type: String},
        isDisabled:{type: Boolean, default: false }
    },
    emits:['handleClick'],
    methods:{
        handleClick() : void{
            this.$emit('handleClick');
        }
    }
    
})
</script>

<style lang="" scoped>

</style>