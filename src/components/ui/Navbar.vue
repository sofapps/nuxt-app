<template>
    <nav ref="nav"
        class="mx-auto bg-white z-50 w-full h-[70px] px-2 md:px-24 bg-secondary fixed overflow-hidden flex justify-between items-center shadow-md">
        <NuxtLink to="/">
            Home
        </NuxtLink>
        <div>   
            <NuxtLink to="/about" class="px-4 hover:text-primary ">About</NuxtLink>
            <NuxtLink to="/gallery" class="px-4 hover:text-primary ">Gallery</NuxtLink>
        </div>
        <!-- <NuxtLink to="/blog" class="px-4 hover:text-primary ">Blog</NuxtLink> -->
    </nav>
</template>
<style lang="scss" scoped></style>