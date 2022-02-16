<template>
  <div
    class="relative  font-sans antialiased text-primary-black">
    <div class="min-h-screen flex flex-col ">
        <Navbar class="sticky top-0 bg-white" />
     <div class="flex-1  ">
        <div class="px-8 md:px-4 max-w-6xl mx-auto text-center">
     <div>
       <div class="mt-10">
            <h2 class="text-xl font-semibold flex flex-start">Overview</h2>
              <div class="px-1 mt-6 grid w-full grid-cols-1 gap-4 md:grid-cols-3 xl:gap-[18px] ">
                <div class="shadow rounded-lg py-4 px-4 flex">
                  <div class="flex-1">
                    <p class="text-xs text-gray-400 font-medium flex flex start">
                     Total Assets Supplied
                    </p>
                    <div class="flex mb-1 md:flex-wrap">
                      <h3 class="text-xl text-black-400 font-medium">$1,201,052,129.03</h3>
                      <div class="ml-1  mt-2.5  text-xs text-green-400 font-medium">+3.56%</div>
                    </div>
                    
                  </div>
                    <div class="flex items-center ml-1">
                      <OutgoingIcon  viewBox="0 0 50 50" class="w-10 h-10 fill-current"/>
                    </div>
                  </div>


                <div class="shadow rounded-lg py-4 px-4 flex">
                  <div class="flex-1">
                    <p class="text-xs text-gray-400 font-medium flex flex start">
                     Total Assets Swaped
                    </p>
                    <div class="flex mb-1  mr-1 md:flex-wrap">
                      <h3 class="text-xl text-black-400 font-medium">$205,654,000.53</h3>
                      <div class="ml-1 mt-2.5 text-xs text-red-600 font-medium">-13.56%</div>
                    </div>
                    
                  </div>
                    <div class="flex items-center ml-1">
                      <IncomingIcon viewBox="0 0 50 50" class="w-10 h-10 fill-current"/>
                    </div>
                  </div>

                <div class="shadow rounded-lg py-4 px-4 flex">
                  <div class="flex-1">
                    <p class="text-xs text-gray-400 font-medium flex flex start">
                     Total Assets Borrowed
                    </p>
                    <div class="flex mb-1 mr-1 md:flex-wrap">
                      <h3 class="text-xl text-black-400 font-medium">$205,654,000.53</h3>
                      <div class="ml-1 mt-2.5  text-xs text-red-600 font-medium">-13.56%</div>
                    </div>
                    
                  </div>
                    <div class="flex items-center ml-1">
                      <IncomingIcon viewBox="0 0 50 50" class="w-10 h-10 fill-current"/>
                    </div>
                  </div>



              </div>

            <Transactions/>
        </div>
     </div>
        </div>
        
     </div>
    </div>
  </div>
  
</template>

<script>
import OutgoingIcon from "~/assets/img/outgoing.svg?inline";
import IncomingIcon from "~/assets/img/incoming.svg?inline";
import Transactions from "~/components/Transactions.vue";

export default {
   layout: 'custom',
  components :{
          OutgoingIcon,
          IncomingIcon,
          Transactions
        },
  name: 'IndexPage',
}
</script>
<style>

</style>

