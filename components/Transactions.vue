<template>
  <div class="pt-5 mb-10">
    <h1 class="flex flex-start text-gray-400 text-lg mb-2">Recent Transactions</h1>

    <div class=" rounded-md shadow hidden md:block">
      <table class="w-full font-semibold">
        <thead class=" border-b-2 border-gray-200">
        <tr class="text-gray-400">
          <th class=" p-3 pl-5 w-32  text-sm font-semibold tracking-wide text-left">DSA ID</th>
          <th class="p-3 w-40 text-sm font-semibold tracking-wide text-left">Action</th>
          <th class=" p-3 text-sm font-semibold tracking-wide text-left">Token</th>
          <th class=" p-3  w-32 text-sm font-semibold tracking-wide text-left">Total Value</th>
          <th class=" p-3 w-32 text-sm font-semibold tracking-wide text-left">Token Amount</th>
          <th class=" p-3 w-32 text-sm font-semibold tracking-wide text-left">Token Amount</th>
          <th class=" p-3 text-sm font-semibold tracking-wide text-left">Transaction Link</th>
        </tr>
        </thead>

        <tbody class="divide-y divide-gray-100">  

        <tr v-for="tran in trans" :key="tran.dsa_id" class="bg-white">
          <td class="p-2.5 pl-5 text-sm text-gray-400 font-bold whitespace-nowrap text-left">#{{tran.dsa_id}}</td>

          <td class="p-2.5 text-xs whitespace-nowrap text-left">
             <span v-if="tran.action ==='SWAP'"
            class="flex w-24 h-6 justify-center items-center  font-medium uppercase tracking-wider text-white bg-blue-600 rounded-md bg-opacity-70">{{tran.action}}</span>
            <span v-if="tran.action ==='SUPPLIED'"
            class="flex w-24 h-6 justify-center items-center text-xs font-medium uppercase tracking-wider text-white bg-green-400 rounded-md ">{{tran.action}}</span>
            <span v-if="tran.action ==='BORROW'"
            class="flex w-24  h-6 justify-center items-center text-xs font-medium uppercase tracking-wider text-white bg-yellow-500 rounded-md bg-opacity-80">{{tran.action}}</span>
          </td>

          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">{{tran.token}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">${{tran.total_value}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">{{tran.token_amount_to}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">{{tran.token_amount_from}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">
            <a :href="tran.link" class="font-bold text-blue-500 hover:underline flex">{{tran.link.slice(8,30)}}...<ExternalLinkIcon class="w-4 h-4"/></a>
            </td>
           
        </tr>
        <tr>
            <td colspan="7"> <div class=" flex w-full justify-center h-10 items-center"><LeftIcon class="w-3 h-3 text-blue-200 mr-4"/>Page 1 of 7<RightIcon class="w-3 h-3 text-blue-600 ml-4"/></div></td>
        </tr>
        </tbody>
      </table>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 md:hidden">

      <div v-for="tran in trans" :key="tran.dsa_id" class="bg-white space-y-3 p-4 rounded-lg shadow font-semibold">
        <div class="flex items-center m-auto space-x-8 text-sm  w-64">
          <div class="text-sm text-gray-400 font-bold whitespace-nowrap">#{{tran.dsa_id}}</div>
          <div class="text-sm text-gray-700 whitespace-nowrap">{{tran.token}}</div>
          <div>
           <div>${{tran.total_value}}</div>
          </div>
        </div>
         <div class="flex m-auto space-x-4 text-sm h-6 p-auto w-64">
           <div class="w-10" v-if="tran.token_amount_to===''"> </div>
          <div class="text-sm text-gray-700 whitespace-nowrap">{{tran.token_amount_to}}</div>

          <div class="text-sm text-gray-700 whitespace-nowrap">             
            <span v-if="tran.action ==='SWAP'"
            class="flex w-24 h-6 justify-center items-center  text-xs font-medium uppercase tracking-wider text-white bg-blue-600 rounded-md bg-opacity-70">{{tran.action}}</span>
            <span v-if="tran.action ==='SUPPLIED'"
            class="flex w-24 h-6 justify-center items-center text-xs font-medium uppercase tracking-wider text-white bg-green-400 rounded-md ">{{tran.action}}</span>
            <span v-if="tran.action ==='BORROW'"
            class="flex w-24  h-6 justify-center items-center text-xs font-medium uppercase tracking-wider text-white bg-yellow-500 rounded-md bg-opacity-80">{{tran.action}}</span>
          </div>

          <div>
           <div class="text-sm text-gray-700 whitespace-nowrap ">{{tran.token_amount_from}}</div>
          </div>
        </div>

        <div class="text-sm font-medium text-black m-auto  w-68" >
         <a :href="tran.link" class="font-bold text-blue-500 hover:underline m-auto  w-64 flex">{{tran.link.slice(8,40)}}...<ExternalLinkIcon class="w-4 h-4"/></a>
        </div>
       
      </div>

       <div class=" sm:col-span-2  flex w-full justify-center h-10 items-center"><LeftIcon class="w-3 h-3 text-blue-200 mr-4"/>Page 1 of 7<RightIcon class="w-3 h-3 text-blue-600 ml-4"/></div>
    </div>


  </div>
</template>

<script>


import { defineComponent } from '@vue/composition-api'
import ExternalLinkIcon from "~/assets/img/external-link.svg?inline";
import LeftIcon from "~/assets/img/arrow-left.svg?inline";
import RightIcon from "~/assets/img/arrow-right.svg?inline";


export default defineComponent({
  components:{
    ExternalLinkIcon,
    LeftIcon,
    RightIcon,
  },
    setup() {

      const trans = [
        {
          dsa_id:"71242",
          action:"SWAP",
          token:"ETH to AVAX",
          total_value:"2,45m",
          token_amount_to:"5.4k ETH",
          token_amount_from: "64.4k AVAX",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
        },
        {
          dsa_id:"71243",
          action:"SUPPLIED",
          token:"LEND",
          total_value:"2,45m",
          token_amount_to:"5.4k ETH",
          token_amount_from:"",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
        },
        {
          dsa_id:"71244",
          action:"SWAP",
          token:"ETH to AVAX",
          total_value:"2,45m",
          token_amount_to:"5.4k ETH",
          token_amount_from: "64.4k AVAX",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
         },
          {
          dsa_id:"71245",
          action:"BORROW",
          token:"DAI",
          total_value:"2,45m",
          token_amount_to:"",
          token_amount_from: "64.4k DAI",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
        },
        {
          dsa_id:"71242",
          action:"SWAP",
          token:"ETH to AVAX",
          total_value:"2,45m",
          token_amount_to:"5.4k ETH",
          token_amount_from: "64.4k AVAX",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
        },
        {
          dsa_id:"71243",
          action:"SUPPLIED",
          token:"LEND",
          total_value:"2,45m",
          token_amount_to:"5.4k LEND",
          token_amount_from:"",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
        },
        {
          dsa_id:"71244",
          action:"SWAP",
          token:"ETH to AVAX",
          total_value:"2,45m",
          token_amount_to:"5.4k ETH",
          token_amount_from: "64.4k AVAX",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
         },
          {
          dsa_id:"71245",
          action:"BORROW",
          token:"DAI",
          total_value:"2,45m",
          token_amount_to:"",
          token_amount_from: "64.4k DAI",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
        },
          {
          dsa_id:"71245",
          action:"BORROW",
          token:"DAI",
          total_value:"2,45m",
          token_amount_to:"",
          token_amount_from: "64.4k DAI",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
        },
          {
          dsa_id:"71246",
          action:"BORROW",
          token:"DAI",
          total_value:"2,45m",
          token_amount_to:"",
          token_amount_from: "64.4k DAI",
          link: "https://etherscan.io/tx/0xdb80c6a86be4f1fa18dfd235df54b78d3eea8909f024614df46f1aae746f599f"
        },

      ] 


      return{
        trans
      };
    },
})
</script>
