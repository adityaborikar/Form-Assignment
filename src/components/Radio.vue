<template>
    <div>
        <label class="label cursor-pointer">
            <span class="label-text mr-2">{{ label }}</span>
            <input type="radio" :value="value" :name="name" class="radio "
                @change="$emit('update:modelValue', $event.target.value)" />
        </label>
    </div>
</template>


<script setup>
defineProps({
    genderName: String,
    label: String,
    name: String,
    modelValue: {
        type: [String],
        default: "",
    },
})
</script>