<template>
    <div>
        <select id="selectedCity" class="select select-bordered w-full max-w-xs">
            <option disabled selected>Select City</option>
            <option>Han Solo</option>
        </select>
    </div>
</template>
<script setup>
defineProps({
    genderName: String,
    genderId: String,
})
const cities = [
    { name: "Mumbai" }, { name: "Nagpur" }
]

cities.forEach((city) => {
    let data = document.createElement("option")
    data.text = cities.name;
    selectedCity.appendChild(data)
})
</script>