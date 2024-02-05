<template>
  <aside>
    <div
      class="flex h-full w-full flex-col gap-5 overflow-y-auto text-white p-5"
    >
      <div class="flex justify-end lg:hidden">
        <img
          src="https://api.iconify.design/mdi:close-thick.svg?color=%23ffffff"
          alt=""
          class="h-8 w-8 border-2 rounded-full p-1`"
          @click="() => handleShow()"
        />
      </div>
      <NuxtLink
        to="/"
      >
        <div class="lg:text-3xl text-2xl font-bold">
          Visa Indonesia
        </div>
      </NuxtLink>

      <SidebarItem :links="menu" @click="() => handleShow()" />

      <div class="mt-auto border-t pt-4 border-slate-200/50 flex justify-between">
        <div class="flex space-x-3">
          <div>
            <img 
              src="/administrator.jpg"
              class="bg-white rounded-full w-12 h-12 object-cover"
              alt=""
            />
          </div>
          <div class="my-auto">
            <div class="font-medium text-sm">Administrator</div>
            <div class="text-xs">admin@spdigital.com</div>
          </div>
        </div>
        <img 
          @click="toggleModal('openModalLogout')"
          src="https://api.iconify.design/ic:baseline-logout.svg?color=%23ffffff" 
          alt="" 
          class="w-8 h-8 bg-primary hover:bg-[#344155] rounded-md p-1 my-auto"
        />
      </div>
    </div>

    <!-- modal window for logout -->
    <Popup 
      v-if="modalTrigger.openModalLogout" 
      :toggleModal="() => toggleModal('openModalLogout')"
    >
      <div class="w-full flex justify-center">
        <img src="/question.png" alt="" class="w-32 h-32 object-cover"/>
      </div>
      <div class="text-center">Are you sure want to logout?</div>
      <div class="flex w-full justify-between space-x-5">
        <button @click="toggleModal('openModalLogout')" class="bg-red-400 rounded-lg px-4 py-2 w-[50%] font-bold text-white hover:shadow-inner">No.</button>
        <button @click="toggleModal('openModalLogout')" class="bg-blue-400 rounded-lg px-4 py-2 w-[50%] font-bold text-white hover:shadow-inner">Yes, logout.</button>
      </div>
    </Popup>
  </aside>
</template>
  
<script setup lang="ts">
  const {handleShow} = defineProps<{
    handleShow?: any,
  }>();
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

  const modalTrigger = ref({
    openModalLogout: false,
  })

  const toggleModal = (e: any) => {
    modalTrigger.value[e] = !modalTrigger.value[e]
  }
</script>