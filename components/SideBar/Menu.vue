<template>
<div class="flex flex-col">
        <header class="flex items-center gap-2 p-4 hover:scale-[101%] transition cursor-pointer">
            <Logo/>
            <div class="font-bold">Nuxt-Finance</div>
        </header>
        <div class="grow px-4">
            <div class="grid gap-4">
                <NuxtLink v-for="(item, index) in items" :key="index" :to="item.path" class="flex items-center gap-2 px-2 py-1 transition rounded cursor-pointer hover:bg-neutral-100">
                    <icon size="20" :name="item.icon" color="black"/>
                    <span>{{ item.title }}</span>
                </NuxtLink>
            </div>
        </div>
</div>
</template>

<script setup>
    const items = ref([
        {
            title: 'Overview',
            path: "/",
            icon: "ri:dashboard-line",
        },
        {
            title: 'Transactions',
            path: "/transactions",
            icon: "nimbus:money",
        },
        {
            title: 'Account',
            path: "/account",
            icon: "line-md:account",
        },
        {
            title: 'Contacts',
            path: "/contacts",
            icon: "mingcute:contacts-2-line",
        },
        {
            title: 'Settings',
            path: "/settings",
            icon: "solar:settings-outline",
        }
    ])

</script>

<style scoped>

</style>