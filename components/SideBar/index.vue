<template>
  <div>
    <!-- Header for smaller screens -->
    <div
      class="flex lg:hidden z-50 items-center justify-between w-full h-full p-4">
      <Logo />
      <div>
        <Icon
          class="z-50 cursor-pointer left-2 top-2"
          size="30"
          name="mdi-light:menu"
          @click="open = true" />
      </div>
      <div v-if="open" class="fixed top-0 left-0 z-50 w-full h-screen bg-white">
        <Icon
          class="absolute z-50 cursor-pointer right-4 top-4"
          size="30"
          name="iconamoon:close-thin"
          @click="open = false" />
        <SideBarMenu/>
      </div>
    </div>
    <!-- Sidebar and content for larger screens -->
    <div
      class="hidden lg:flex w-[250px] h-screen flex-col justify-between border-r">
      <SideBarMenu />
      <div>UserItem</div>
    </div>
  </div>
</template>

<script setup>
const open = ref(false);
</script>

<style scoped></style>
