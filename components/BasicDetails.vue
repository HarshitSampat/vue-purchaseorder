<script setup>
const props = defineProps(['data', 'heading'])
</script>
<template>
    <div class="text-gray-800 text-[15px]">
        <h2 class="font-medium text-black">{{ heading }}</h2>
        <template v-for="(value, key) in data">
            <p v-if="(typeof value==='object')">
                <p v-for="(val, k) in value">{{val}}</p>
            </p>
            <p v-else>{{value}}</p>
            <!-- <p>{{ Object.values(data)[0] }}</p>
            <p>{{ Object.values(data)[1].Line1 }}</p>
            <p>{{ Object.values(data)[1].Line2 }}</p>
            <p>{{ Object.values(data)[1].CityState }}</p>
            <p>{{ data.Contact.Name }}, {{ data.Contact.Number }}</p>
            <p>{{ data.Contact.Email }}, {{ data.Contact.Website }}</p>
            <p><strong>{{ Object.keys(data)[3] }}: </strong><span>{{ Object.values(data)[3] }}</span></p>
            <p><strong>{{ Object.keys(data)[3] }}: </strong><span>{{ Object.values(data)[4] }}</span></p> -->
        </template>
    </div>
</template>