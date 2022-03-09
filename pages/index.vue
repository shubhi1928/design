<template>
  <div
    class="relative  font-sans antialiased text-primary-black bg-gray-100">
    <div class="min-h-screen flex flex-col ">

 



        <div v-if="check_balance===false">

          <div class="flex justify-center items-center h-screen"> 

               <div class="flex flex-col justify-center items-center w-[400px] h-[500px] bg-white rounded-md shadow">

        <InstadappIcon  class="w-16 h-16 text-white mb-4"/>
      <div class="ml-2 font-extrabold text-xl">LOGIN</div>



               <p class="mt-12 font-semibold text-gray-500 text-lg"> Connect with wallet</p>
                  <button @click="onconnect" class="w-[250px] bg-blue-500 h-[40px] border-2 rounded-md p-auto text-white mt-2">Connect wallet</button>


                  <p class="mt-8 font-semibold text-gray-500 text-lg">Check balance of any walllet</p>
                   <SearchInput
            dense
            class="mt-2 w-[250px]"
            placeholder="Enter wallet Address"
            v-model="walletAddress" @change="allbalance"
          />


            </div>


          </div>

          



          
          </div>




      
      <div v-else>
      
       <div class="sticky top-0 bg-white px-4 md:px-8 py-4 border border-b-[#E7E8F1] shadow flex flex-col md:flex-row md:items-center md:justify-between ">
    <div class="flex items-center ">
        <InstadappIcon  class="w-8 h-8 text-white"/>
      <span class="ml-2 font-extrabold text-lg">EXPLORER</span>
    </div>
      
      <div class="mt-4  sm:mr-1 flex  items-center ">
        
        <button v-if ="check_myaddress===false" @click="onconnect" class="w-[300px] bg-blue-500 h-[45px] border-2 rounded-md p-auto text-white mr-4 text-sm">Connect wallet</button>
        <button v-else @click="onconnect1" class="w-[150px] bg-blue-500 h-[42px] border-2 rounded-md p-auto text-white mr-4 text-sm">Check my balance</button>

          <SearchInput
            dense
            class="w-[300px] h-[45px]"
            placeholder="Enter wallet Address"
            v-model="walletAddress" @change="allbalance"
          />
          <select v-model="net" @change="allbalance"  class="w-[150px] h-[45px] ml-2 rounded-lg border-2 border-gray-300 text-gray-500">  
          <option class=" rounded-lg border-2 border-gray-300 text-gray-500">mainnet</option>
          <option class=" rounded-lg border-2 border-gray-300 text-gray-500">polygon</option>

</select>

        </div>
      
          </div>

     <div class="flex-1 ">
        <div class="px-8 md:px-4 max-w-6xl mx-auto text-center">
     <div >
       <div class="mt-10">

           <h2 class="text-xl font-semibold flex flex-start ">Overview </h2>
  
            


              <div class="px-1 mt-6 grid w-full grid-cols-1 gap-4 md:grid-cols-3 xl:gap-[18px] ">
                    
                  <div class="shadow rounded-lg py-4 px-4 flex border-gray-400 border-2 bg-white">
                  <div class="flex-1">
                    <p class="text-sm text-gray-400 font-medium flex flex start">
                      Net Worth in USD
                    </p>
                    <div class="flex mb-1 md:flex-wrap">
                      <h3 class="text-xl text-black-400 font-medium"><span class=" font-bold text-gray-400 ">$</span>   {{parseFloat(totalUsd).toFixed(3)}}</h3>
                    </div>

                  </div>
                    <div class="flex items-center ml-1">
                      <DollarIcon class="w-8 h-8"/>
                    </div>
                  </div>

                  
                  <div class="shadow rounded-lg py-4 px-4 flex border-gray-400 border-2 bg-white">
                  <div class="flex-1">
                    <p class="text-sm text-gray-400 font-medium flex flex start">
                      Net Worth in ETH
                    </p>
                    <div class="flex mb-1 md:flex-wrap">
                      <h3 class="text-xl text-black-400 font-medium"><span class=" font-bold text-gray-400 "> ETH</span>   {{parseFloat(totalETH).toFixed(3)}}</h3>
                    </div>

                  </div>
                    <div class="flex items-center ml-1">
                      <EthIcon class="w-8 h-8"/>
                    </div>
                  </div>



                <div class="shadow rounded-lg py-4 px-4 flex border-gray-400 border-2 bg-white">
                  <div class="flex-1">
                    <p class="text-sm text-gray-400 font-medium flex flex start">
                     Total Balance Change (24H)
                    </p>
   
                    
                  </div>
                  </div>



              </div>

            <div class="pt-5 mb-10">
   <div class="flex place-content-between">
     <div class="flex mb-2">
       <h1 class="flex flex-start text-black-400 text-lg font-semibold">Assets in wallet</h1>
       <a target="_blank" :href="getwallet()" class="text-blue-600 font-semibold">({{walletAddress.slice(0,5)}}...{{walletAddress.slice(-4)}})</a>
     </div>
  
         
        </div> 

    <div v-if ="check_balance===true" class=" rounded-md shadow  border-gray-400 border-2  overflow-auto">
      <table class="w-full font-semibold">
        <thead class=" border-b-2 border-gray-400">
        <tr class="text-gray-400 bg-white">
          <th class=" p-3 pl-5 w-40  text-sm font-semibold tracking-wide text-left">Assets</th>
          <th class=" p-3 w-40 text-sm font-semibold tracking-wide text-left">Symbol</th>
          <th class=" p-3  w-40 text-sm font-semibold tracking-wide text-left">Quantity</th>
          <th class=" p-3 w-40 text-sm font-semibold tracking-wide text-left">Price</th>
          <th class=" p-3 w-40 text-sm font-semibold tracking-wide text-left">Value</th>
          <th class=" p-3 text-sm font-semibold tracking-wide text-left">Contract address</th>
        </tr>
        </thead>

        <tbody class="divide-y divide-gray-100">  

        <tr v-for="tran in trans" :key="tran.coin_id" class="bg-white">
          <td class="p-2.5 pl-5 text-sm text-gray-400 font-bold whitespace-nowrap text-left">{{tran.assets}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap ">    
             <component :is="tran.symbol" class="w-6 h-6 ml-3" />
             </td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">{{parseFloat(tran.quantity).toFixed(3)}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">${{parseFloat(tran.price).toFixed(3)}}</td>
          <td class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">${{parseFloat(tran.value).toFixed(3)}}</td>

          <td   v-if="net=='mainnet'" class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">
            <a  target="_blank" :href="getaddress(tran.contractaddress)" class="font-bold text-blue-500 hover:underline flex">{{tran.contractaddress.slice(0,30)}}...<ExternalLinkIcon class="w-4 h-4"/></a>


          </td>
          <td v-else class="p-2.5 text-sm text-gray-700 whitespace-nowrap text-left">
            <a v-if="tran.coin_id!='ethereum'" target="_blank" :href="getaddress(tran.contractaddress_polygon)" class="font-bold text-blue-500 hover:underline flex">{{tran.contractaddress_polygon.slice(0,30)}}...<ExternalLinkIcon class="w-4 h-4"/></a>
          </td>
           
        </tr>
        <tr>
            <td colspan="7"> <div class=" flex w-full justify-center h-10 items-center bg-white"><LeftIcon class="w-3 h-3 text-blue-200 mr-4"/>Page 1 of 7<RightIcon class="w-3 h-3 text-blue-600 ml-4"/></div></td>
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
        </div>
     </div>
        </div>
        
     </div>
     </div>
    </div>
  </div>
  
</template>

<script>

import { defineComponent } from '@vue/composition-api'
import ExternalLinkIcon from "~/assets/img/external-link.svg?inline";
import LeftIcon from "~/assets/img/arrow-left.svg?inline";
import RightIcon from "~/assets/img/arrow-right.svg?inline";
import OutgoingIcon from "~/assets/img/outgoing.svg?inline";
import IncomingIcon from "~/assets/img/incoming.svg?inline";
import InstadappIcon from "~/assets/img/instadapp-logo-icon.svg?inline";
import DollarIcon from "~/assets/img/dollar.svg?inline";


import DaiIcon from "~/assets/img/dai.svg?inline";
import UsdtIcon from "~/assets/img/usdt.svg?inline";
import InstIcon from "~/assets/img/inst.svg?inline";
import UsdcIcon from "~/assets/img/usdc.svg?inline";
import EthIcon from "~/assets/img/eth.svg?inline";
import WethIcon from "~/assets/img/weth.svg?inline";
import WbtcIcon from "~/assets/img/wbtc.svg?inline";
import MaticIcon from "~/assets/img/matic.svg?inline";
import Web3 from "web3";
import Web3Modal from "web3modal";
import WalletConnectProvider from "@walletconnect/web3-provider";
import VueCookies from 'vue-cookies';



// import Web3 from 'web3';


export default defineComponent({
  components:{
    ExternalLinkIcon,
    LeftIcon,
    RightIcon,
    OutgoingIcon,
    IncomingIcon,
    InstadappIcon,
    DaiIcon,
    UsdtIcon,
    InstIcon,
    UsdcIcon,
    EthIcon,
    WethIcon,
    WbtcIcon,
    MaticIcon,
    DollarIcon,
    Web3,
    Web3Modal,
    WalletConnectProvider,
    VueCookies
    
  },
    setup() {
      

      const Web3 = require('web3');
      const CoinGecko = require('coingecko-api');
      var check_balance = false
      var check_myaddress = false
      var net ="mainnet"
 
      
      var my_address
      
        if(VueCookies.isKey('check_balance'))
        {
          check_balance=VueCookies.get('check_balance')
        }
         if(VueCookies.isKey('check_myaddress'))
        {
          check_myaddress=VueCookies.get('check_myaddress')
        }
         if(VueCookies.isKey('my_address'))
        {
          my_address=VueCookies.get('my_address')
        }

        // VueCookies.remove("my_address")
        // VueCookies.remove("check_myaddress")
        // VueCookies.remove("check_balance")

      var walletAddress=""
      var totalUsd = 0
      var totalETH = 0

      var trans = [
        {
          assets:"Ethereum (ETH)",
          symbol:EthIcon,
          quantity:"0",
          price:"0",
          value:"0",
          contractaddress:"0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
          contractaddress_polygon:"0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
          coin_id:"ethereum",
          decimals:18

        },
         {
          assets:"INSTADAPP (INST)",
          symbol:InstIcon,
          quantity:"0",
          price:"0",
          value:"0",
          contractaddress:"0x6f40d4A6237C257fff2dB00FA0510DeEECd303eb",
          contractaddress_polygon:"0xf50D05A1402d0adAfA880D36050736f9f6ee7dee",
          coin_id:"instadapp",
          decimals:18


        },
         {
          assets:"Wrapped Ether (WETH)",
          symbol:WethIcon,
          quantity:"0",
          price:"0",
          value:"0",
          contractaddress:"0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",
          contractaddress_polygon:"0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619",
          coin_id:"weth",
          decimals:18

        },

         {
          assets:"Dai Stablecoin (DAI)",
          symbol:DaiIcon,
          quantity:"0",
          price:"0",
          value:"0",
          contractaddress:"0x6B175474E89094C44Da98b954EedeAC495271d0F",
          contractaddress_polygon:"0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
          coin_id:"dai",
          decimals:18

        },
         {
          assets:"Tether USD (USDT)",
          symbol:UsdtIcon,
          quantity:"0",
          price:"0",
          value:"0",
          contractaddress:"0xdAC17F958D2ee523a2206206994597C13D831ec7",
          contractaddress_polygon:"0xc2132D05D31c914a87C6611C10748AEb04B58e8F",
          coin_id:"tether",
          decimals:6

        },
         {
          assets:"USD Coin (USDC)",
          symbol:UsdcIcon,
          quantity:"0",
          price:"0",
          value:"0",
          contractaddress:"0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
          contractaddress_polygon:"0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174",
          coin_id:"usd-coin",
          decimals:6

          

        },
         {
          assets:"Wrapped BTC (WBTC)",
          symbol:WbtcIcon,
          quantity:"0",
          price:"0",
          value:"0",
          contractaddress:"0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599",
          contractaddress_polygon:"0x1BFD67037B42Cf73acF2047067bd4F2C47D9BfD6",
          coin_id:"wrapped-bitcoin",
          decimals:8

        },
        {
          assets:"Matic Token (MATIC)",
          symbol:MaticIcon,
          quantity:"0",
          price:"0",
          value:"0",
          contractaddress:"0x7D1AfA7B718fb893dB30A3aBc0Cfc608AaCfeBB0",
          contractaddress_polygon:"0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
          coin_id:"matic-network",
          decimals:18

        },
        





      ]

      function getaddress(contract){
        if(this.net=='mainnet')
        {
  
        return "https://etherscan.io/token/"+contract
        }
        else
        {
          return "https://polygonscan.com/token/"+contract
        }
      }
      function getwallet(){
        if(this.net=='mainnet')
        {
        return "https://etherscan.io/tokenholdings?a="+this.walletAddress
        }
        else
        {
        return "https://polygonscan.com/tokenholdings?a="+this.walletAddress
        }
      }


      async function getprice(ArrayOfcoin_id){

        
        const CoinGeckoClient = new CoinGecko();

        var price = await CoinGeckoClient.simple.price({
                ids: ArrayOfcoin_id,
                vs_currencies: ['usd'],
            });

            return price;

      }



      async function getbalanceERC20_all(walletAddress,ArrayOfTokenAddress){
              var Web3Client
              if(this.net=='mainnet')
              {
               Web3Client = new Web3(new Web3.providers.HttpProvider("https://mainnet.infura.io/v3/5a30774b8e5143fabbbb8e724b671741"));
              }
              else 
              {
                 Web3Client = new Web3(new Web3.providers.HttpProvider("https://polygon-rpc.com/"));
              
              }
              const ABI = [
                {
                  "inputs":[{"internalType":"address","name":"owner","type":"address"},
                            {"internalType":"address[]","name":"tknAddress","type":"address[]"}],

                  "name":"getBalances",

                  "outputs":[{"internalType":"uint256[]","name":"","type":"uint256[]"}],

                  "stateMutability":"view",

                  "type":"function"
                  
                  },

              ]
              var resolverAddress
              if(this.net=='mainnet')
              {
              resolverAddress = "0x5b7D61b389D12e1f5873d0cCEe7E675915AB5F43"
              }
              else
              {
              resolverAddress = "0x58632D23120b20650262b8A629a14e4F4043E0D9"
              }




              const contract = new Web3Client.eth.Contract(ABI, resolverAddress);

              const balances = await contract.methods.getBalances(walletAddress,ArrayOfTokenAddress).call();

              return balances
      }
   

    async function allbalance( check_self = false){

      if(check_self===true){
           if(window.ethereum.networkVersion==137){
                this.net = 'polygon'
            }
            else{
              this.net = "mainnet"
            }

      }

       

      console.log(this.walletAddress)

            this.totalUsd = 0

            var ArrayOfTokenAddress =[]
            
            for(var i =0; i <this.trans.length; i++)
            {
              if(this.net=='mainnet')
              {
              ArrayOfTokenAddress.push(this.trans[i].contractaddress)
              }
              else
              {
              ArrayOfTokenAddress.push(this.trans[i].contractaddress_polygon)
              }
            }

            var quantity = await this.getbalanceERC20_all(this.walletAddress,ArrayOfTokenAddress)
            

            for(var i =0; i <trans.length; i++){
                      
                      this.trans[i].quantity =  quantity[i] / 10**trans[i].decimals


                }
                if(this.net=='polygon')
                {
                  this.trans[0].quantity=0
                }
     

            var ArrayOfcoin_id=[]

            for(var i =0; i <this.trans.length; i++){
               ArrayOfcoin_id.push(this.trans[i].coin_id)
            }


            var price1 = await getprice(ArrayOfcoin_id)
            
    
            for(var i =0; i <this.trans.length; i++){
                      this.trans[i].price =  price1.data[trans[i].coin_id].usd
                }



            for(var i =0;i<trans.length;i++){

                  trans[i].value = trans[i].price*trans[i].quantity               
                  this.totalUsd += trans[i].value 

            }


            this.totalETH = this.totalUsd/ this.trans[0].price;

            this.check_balance = true
            VueCookies.set('check_balance',true,'1h')
    }

    async function collect()
    {
     

          const providerOptions = {
                    /* See Provider Options Section */
                    walletconnect: {
            package: WalletConnectProvider, // required
            options: {
              infuraId: "5a30774b8e5143fabbbb8e724b671741" // required
          }
            },
            binancechainwallet: {
              package: true
            }
          };

          const web3Modal = new Web3Modal({
            network: this.net, // optional
            cacheProvider: false, // optional
            providerOptions // required
          });

          const provider = await web3Modal.connect();

          const Myweb3 = new Web3(provider);
          const accounts = await Myweb3.eth.getAccounts()
           return(accounts[0])
    }


    async function onconnect(){


      var address = await this.collect();
      console.log(address)
      this.walletAddress = address;

      this.my_address = address;


     


      await this.allbalance( true);
      this.check_myaddress = true

      VueCookies.set('check_myaddress',true,'1h')
      VueCookies.set('my_address',address,'1h')
      


    }

    async function onconnect1(){

      this.walletAddress = this.my_address
      await this.allbalance();

    }

    




    


     
      return{trans,walletAddress,getbalanceERC20_all,allbalance,totalUsd,totalETH,getaddress,getwallet,check_balance,collect,onconnect,check_myaddress,my_address,onconnect1,net
        
      };
    },
})

</script>
<style scoped>


</style>


