<script lang="ts">
	import { Pop } from "$lib/utilities/popup";
    import Modal from "$lib/components/Modal.svelte";
    import axios from "axios";


    const pop = new Pop()

    let RequestQuoteData = {}
    let busy:boolean

    const RequestQuote = async ()=>{
        try {
            console.log('test');
            
            busy=true;
            const response = await axios.post('/api/quote',RequestQuoteData)
            console.log(response);
            
            if(response.status==201){
                busy = false;
                alert("Quote submitted!!")
                RequestQuoteData = {}
                return
            } 
            alert("something went wrong!!!")           
        } catch (error) {
            alert(error)
            
        }
   
    }

    export let data;
    console.log(data);

    let products = data.data.results


        
</script>



<h2 class=" mt-[8rem] lg:mt-[10rem] text-center text-2xl lg:text-4xl font-bold">Vaccine Cold Chain Solutions</h2>


<div class="  bg-white py-[2rem] mt-[1rem] lg:mt-[2rem] px-3 lg:p-[4rem] shadow-md">
    <span>
        Our range of offerings is aimed at minimizing the total cost of ownership and ensuring the vaccine's efficacy
        all the way to the final destination, even in extremely challenging conditions. Our product line consists of ice-lined
        refrigerators and freezers suitable for health centers facing power instability, solar-powered vaccine storage equipment,
        and durable transport systems that maintain cold temperatures for extended periods during lengthy journeys.
    </span>
</div>



  
  <div class="container pb-[4rem]">
    {#each products as item}
      <div class="product-card">
        <img src="{item.image}" alt="{item.name}">
        <h2 class="product-name text-[1.4rem] text-[#23286b]">{item.name}</h2>
        
        <div class="product-quote">
            <p class=" ">{item.description}</p>
          <button class="quote-button" on:click={()=>{pop.ToggleWind('quote','flex')}}>Request a Quote</button>
        </div>
      </div>
    {/each}
  </div>



<Modal  modalid='quote'>
    <div class="modalfix flex flex-col gap-4 mx-[1rem] lg:mx-[4rem] lg:mb-[1rem] p-0 lg:p-3">

        <h1 class='text-[#23286b] text-center font-bold text-lg lg:text-[1.88rem]'>Request a Quote</h1>

        <div class='flex  flex-col gap-1 lg:gap-1 lg:items-center'>
            <span class="font-light text-xs text-center lg:text-base lg:p-1">
                At Prezzo, we can help you find the best prices and availability for your needs with our network of verified suppliers.
            </span>
            <span class="font-light text-xs text-center lg:p-1 lg:text-base">
                We can provide 1000 cases of gloves delivered tomorrow or establish a contract with a respirator manufacturer for the next year.
            </span>
            <span class="font-light text-xs text-center lg:p-1 lg:text-base">
                Fill out your information below and we'll find the right suppliers for you. With Prezzo, you can trust you're getting the best pricing and availability.
            </span>
            <!-- <span class="font-light text-xs text-center lg:p-1 lg:text-base">
                Please fill out the form below and we'll get back to you as soon as possible.
            </span> -->
        </div>
        

        <form on:submit|preventDefault={RequestQuote} class="flex flex-col gap-2">
            <div class="flex flex-col gap-2">
                <span class="text-[#23286b] text-lg font-semibold">Name</span>
                <input bind:value={RequestQuoteData.full_name} type="text" class="w-full h-[2.5rem] border border-[#23286b] p-3" required>
            </div>

            <div class="flex flex-col gap-2 w-full lg:flex-row">
                <div class="flex flex-col gap-2 w-full">
                    <span class="text-[#23286b] text-lg font-semibold">Email</span>
                    <input bind:value={RequestQuoteData.email} type="email" class="w-full h-[2.5rem] border border-[#23286b] p-3" required>
                </div>

                <div class="flex flex-col gap-2 w-full">
                    <span class="text-[#23286b] text-lg font-semibold">Phone number</span>
                    <input bind:value={RequestQuoteData.phone_number} type="phone" class="h-[2.5rem] border border-[#23286b] p-3" required>
                </div>
            </div>


            <div class="flex flex-col gap-2">
                <span class="text-[#23286b] text-lg font-semibold">What can we help you with</span>

                <textarea bind:value={RequestQuoteData.message} name="" id=""  class="w-full h-[6rem] border border-[#23286b] p-3" required></textarea>
            </div>

            {#if !busy}
                    <button type="submit" class="h-[2.5rem] w-[10rem] bg-[#23286b] text-white">Sumbit Quote</button>

            {:else}
                  <button disabled type="submit" class="h-[2.5rem] w-[10rem] bg-[#23286b] text-white flex justify-center items-center"><i class='bx bx-loader bx-spin text-white text-[1rem]' ></i></button>

            {/if}

        </form>

    </div>

</Modal>


  






  
  


<style>
    .container {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 2rem;
      margin: auto;
      margin-top: 6rem;
    }
  
    .product-card {
      position: relative;
      display: flex;
      flex-direction: column;
      align-items: center;
      border: 1px solid #ccc;
      border-radius: 0.5rem;
      padding: 1rem;
      transition: transform 0.3s ease;
    }
  
    .product-card:hover {
      transform: translateY(-0.5rem);
      background-color: #f8f8f8;
    }
  
    .product-card img {
      width: 20rem;
      height: 17rem;
      object-fit: contain;
      margin-bottom: 1rem;
      transition: transform 0.3s ease;
    }
  
    .product-card:hover img {
      transform: translateY(-0.5rem);
    }
  
    .product-card h2 {
      color: #23286b;
      font-size: 1.4rem;
      font-weight: 500;
      transition: color 0.3s ease;
      margin-top: -0.5rem;
    }
  
    .product-card:hover h2 {
      color: #23286b;
    }
  
    .product-quote {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      background-color: #f1f1f1;
      border-bottom: 1px;
      border-radius: 0.5rem;
      padding: 1rem;
      display: none;
      transition: transform 0.3s ease;
      transform: translateY(100%);
      z-index: 1;
      text-align: center; /* Added property */
    }
  
    .product-card:hover .product-quote {
      display: flex;
      flex-direction: column;
      align-items: center;
      transform: translateY(0);
    }
  
    .product-card:hover .quote-button {
      background-color: #23286b;
    }
  
    .quote-button {
      background-color: #23286b;
      color: #fff;
      border: none;
      border-radius: 0.3rem;
      padding: 0.5rem 1rem;
      margin-top: 1rem;
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
  </style>
  