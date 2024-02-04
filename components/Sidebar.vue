<template>
  <aside>
    <div
      class="flex h-full w-full flex-col gap-5 overflow-y-auto text-white p-5"
    >
      <NuxtLink
        to="/"
      >
        <div class="text-3xl font-bold">
            Visa Indonesia
        </div>
      </NuxtLink>

      <SidebarItem :links="menu" />

      <div class="mt-auto border-t pt-4 border-slate-200/50 flex justify-between">
        <div class="flex space-x-5">
          <div>
            <img 
              src="/administrator.jpg"
              class="bg-white rounded-full w-12 h-12 object-cover"
              alt=""
            />
          </div>
          <div>
            <div class="">Administrator</div>
            <div>admin@spdigital.com</div>
          </div>
        </div>
        <NuxtLink
          to="/"
          class="flex"
        >
          <img 
            src="https://api.iconify.design/ic:baseline-logout.svg?color=%23ffffff" 
            alt="" 
            class="w-8 h-8 bg-primary hover:bg-[#344155] rounded-md p-1 my-auto"
          />
        </NuxtLink>
      </div>
    </div>
  </aside>
</template>
  
<script setup lang="ts">
  const menu = [
    {
      title: "Dashboard",
      icon: "https://api.iconify.design/bx:home-alt.svg?color=%23ffffff",
    },
    {
      title: "Service",
      icon: "https://api.iconify.design/bx:layer.svg?color=%23ffffff",
    },
    {
      title: "Orders",
      icon: "https://api.iconify.design/bx:book-alt.svg?color=%23ffffff",
    },
    {
      title: "Customer",
      icon: "https://api.iconify.design/tabler:users.svg?color=%23ffffff",
    },
    {
      title: "Customer Identity",
      icon: "https://api.iconify.design/bx:briefcase-alt.svg?color=%23ffffff",
    },
    {
      title: "Promo Code",
      icon: "https://api.iconify.design/bx:purchase-tag.svg?color=%23ffffff",
    },
    {
      title: "Admin User",
      icon: "https://api.iconify.design/bx:user.svg?color=%23ffffff",
    },
  ];
</script>