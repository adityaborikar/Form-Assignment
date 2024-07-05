<template>
    <div class="w-80">
        <label class="label">
            <span class="font-semibold text-slate-600 label-text">{{ label }} <span class="text-red-500">*</span>
            </span>
        </label>
        <label for="">
            <input :type="type" :placeholder="holder" :name="name"
                @input="$emit('update:modelValue', $event.target.value)" class="input input-bordered w-full max-w-xs" />
        </label>
    </div>
</template>

<script setup>
defineProps({
    label: String,
    name: String,
    holder: String,
    errorClass: String,
    modelValue: {
        type: [String, Number],
        default: "",
    },
})
</script>