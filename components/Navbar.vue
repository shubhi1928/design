<template>
  <div class="px-4 md:px-8 py-4 border border-b-[#E7E8F1] shadow flex flex-col md:flex-row md:items-center md:justify-between">
    <div class="flex items-center">
        <InstadappIcon  class="w-8 h-8 text-white"/>
      <span class="ml-2 font-extrabold text-lg">EXPLORER</span>
    </div>
  </div>
</template>
<script>
import { defineComponent } from '@vue/composition-api'
import InstadappIcon from "~/assets/img/instadapp-logo-icon.svg?inline";

export default defineComponent({
     components :{
          InstadappIcon,
        },
    setup() {
        
    },
})
</script>
