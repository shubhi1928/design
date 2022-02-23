<template>
  <div class="pt-5 mb-10">
   <div class="flex place-content-between">
     <h1 class="flex flex-start text-gray-400 text-lg mb-2">Assets in Wallet</h1>
  
          <input type="text" placeholder="Enter wallet Address" class="border-2 mb-2" v-model="walletAddress" @change="allbalance">
         
        </div> 

    <div class=" rounded-md shadow  ">
      <table class="w-full font-semibold">
        <thead class=" border-b-2 border-gray-200">
        <tr class="text-gray-400">
          <th class=" p-3 pl-5 w-32  text-sm font-semibold tracking-wide text-left">Assets</th>
          <th class=" p-3 text-sm font-semibold tracking-wide text-left">Symbol</th>
          <th class=" p-3  w-32 text-sm font-semibold tracking-wide text-left">Quantity</th>
          <th class=" p-3 w-32 text-sm font-semibold tracking-wide text-left">Price</th>
          <th class=" p-3 w-32 text-sm font-semibold tracking-wide text-left">Value</th>
          <th class=" p-3 text-sm font-semibold tracking-wide text-left">Contract address</th>
        </tr>
        </thead>

        <tbody class="divide-y divide-gray-100">  

        <tr v-for="tran in trans" :key="tran.symbol" class="bg-white">
          <td class="p-2.5 pl-5 text-sm text-gray-400 font-bold whitespace-nowrap text-left">{{tran.assets}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">{{tran.symbol}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">{{tran.quantity}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">${{tran.price}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">${{tran.value}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">
            <a :href="tran.link" class="font-bold text-blue-500 hover:underline flex">{{tran.contractaddress.slice(0,30)}}...<ExternalLinkIcon class="w-4 h-4"/></a>
          </td>
           
        </tr>
        <tr>
            <td colspan="7"> <div class=" flex w-full justify-center h-10 items-center"><LeftIcon class="w-3 h-3 text-blue-200 mr-4"/>Page 1 of 7<RightIcon class="w-3 h-3 text-blue-600 ml-4"/></div></td>
        </tr>
        </tbody>
      </table>
    </div>

    
    <!-- <form @submit.prevent="allbalance">
    
    <input v-model="walletAddress"  @change ="allbalance" placeholder="address" >

    </form>
    <p >{{amount[0].balance}}</p>
    <p>{{amount[1].balance}}</p>
     -->


  </div>
</template>

<script>


import { defineComponent } from '@vue/composition-api'
import ExternalLinkIcon from "~/assets/img/external-link.svg?inline";
import LeftIcon from "~/assets/img/arrow-left.svg?inline";
import RightIcon from "~/assets/img/arrow-right.svg?inline";
// import Web3 from 'web3';


export default defineComponent({
  components:{
    ExternalLinkIcon,
    LeftIcon,
    RightIcon,
  },
    setup() {

      var walletAddress=""

      var trans = [
        {
          assets:"Ethereum",
          symbol:"ETH",
          quantity:"0",
          price:"100000",
          value:"0",
          contractaddress:"-",

        },
         {
          assets:"INSTADAPP",
          symbol:"INST",
          quantity:"0",
          price:"1.32",
          value:"0",
          contractaddress:"0x6f40d4A6237C257fff2dB00FA0510DeEECd303eb",

        },
        {
          assets:"BNB",
          symbol:"BNB",
          quantity:"0",
          price:"442",
          value:"0",
          contractaddress:"0xB8c77482e45F1F44dE1745F52C74426C631bDD52",

        },
        {
          assets:"SHIBA INU",
          symbol:"SHIB",
          quantity:"0",
          price:"0.001",
          value:"0",
          contractaddress:"0x95aD61b0a150d79219dCF64E1E6Cc01f0B64C4cE",

        },
        {
          assets:"Matic Token",
          symbol:"MATIC",
          quantity:"0",
          price:"1.55",
          value:"0",
          contractaddress:"0x7D1AfA7B718fb893dB30A3aBc0Cfc608AaCfeBB0",

        },
         {
          assets:"Wrapped Ether",
          symbol:"WETH",
          quantity:"0",
          price:"2655",
          value:"0",
          contractaddress:"0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",

        },




      ]



      async function getBalanceOfERC20(walletAddress,tokenAddress){

         const Web3 = require('web3');
         const Web3Client = new Web3(new Web3.providers.HttpProvider("https://mainnet.infura.io/v3/5a30774b8e5143fabbbb8e724b671741"));

         const minABI = [  
                // balanceOf
                {    
                  constant: true,

                  inputs: [{ name: "_owner", type: "address" }],

                  name: "balanceOf",

                  outputs: [{ name: "balance", type: "uint256" }],

                  type: "function",
                },



              ];

                const contract = new Web3Client.eth.Contract(minABI, tokenAddress);

                const result = await contract.methods.balanceOf(walletAddress).call(); 
  
                const format = Web3Client.utils.fromWei(result); 

                return format
      }


        async function getEth(walletAddress){
          const Web3 = require("web3")

           const web3 = new Web3(new Web3.providers.HttpProvider("https://mainnet.infura.io/v3/5a30774b8e5143fabbbb8e724b671741"))

           const result = await  web3.eth.getBalance(walletAddress);
            const format = web3.utils.fromWei( web3.utils.toBN(result),"ether");
            return format
        }


           async function allbalance(){

             for( var i = 1; i<trans.length;i++){

               var data = await getBalanceOfERC20(this.walletAddress, this.trans[i].contractaddress ).then((balance)=>{
                 this.trans[i].quantity = balance
               })

               this.trans[i].value = this.trans[i].quantity*this.trans[i].price;


             }

             var data1 = await getEth(this.walletAddress).then((balance)=>{
                 this.trans[0].quantity = balance
               })

               this.trans[0].value = this.trans[0].quantity*this.trans[0].price;






             this.walletAddress=""




           }




      




     
      return{trans,walletAddress,getBalanceOfERC20,allbalance,getEth
        
      };
    },
})
</script>
