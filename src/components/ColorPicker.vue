<template>
    <div class="picker-wrapper">
        <label :for="label" class="color-label">{{ label }}</label>
        <input type="color" :value="modelValue" :id="label" @input="inputHandler" class="color-input" />
    </div>
</template>

<script>
export default {
    name: 'ColorPicker',
    props: {
        label: {
            type: String,
            required: true
        },
        modelValue: {
            type: String,
            default: '#000000'
        },
        colors: {
            type: Array,
            required: true,
        }
    },
    methods: {
        inputHandler(event) {
            const newColor = event.target.value;
            const colorIndex = event.target.id.slice(-1) - 1;

            this.$emit('updateColors', colorIndex, newColor);
        }
    }
}
</script>

<style>
.picker-wrapper {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}

.color-label {
    color: #444444;
}

.color-input {
    -webkit-appearance: none;
    appearance: none;
    width: 50px;
    height: 50px;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    outline: none;
    background-color: transparent;
    opacity: 0.7;
    transition: 0.5s;
}

.color-input:hover {
    opacity: 1;
}

.color-input::-webkit-color-swatch {
    border-radius: 50%;
    border: 2px solid #ddd;
}

.color-input::-moz-color-swatch {
    border-radius: 50%;
    border: 2px solid #ddd;
}
</style>