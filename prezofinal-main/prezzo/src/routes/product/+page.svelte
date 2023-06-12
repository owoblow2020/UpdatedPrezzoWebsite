<script>
  import {
    mediaurl
  } from '$lib/config';
  export let data
  console.log(data)
</script>

<div class="carousel-container">
  <div class="carousel">
    {#each data.data as item}
        <a href="/product/{item.id}" class="carousel-item">
        
            <div class="product">
            <h2 class="product-title">{item.name}</h2>
            <a class="product-link" href="/subproduct">View More</a>
            </div>
            <img src="{mediaurl}{item.banner_image}" alt="">
      </a>
      {:else}
      <!-- empty list -->
   {/each}
    </div>
  </div>
  

<div class=" flex flex-col lg:grid lg:grid-cols-2 px-3 py-[2.5rem] lg:py-[4rem] gap-[2rem]">
    {#each data.data as item}
        <div class=" flex flex-col-reverse items-center lg:flex-row lg:justify-center bg-white shadow-lg p-[1.5rem] h-full lg:h-[20rem] w-full rounded-lg">
          <div  class="text-center lg:text-left flex flex-col lg:w-[50%]">
              <h2 class="  text-lg lg:text-xl font-medium lg:font-semibold">{item.name}</h2>
              <span class=" py-[1.5rem]">
                  {item.description}
              </span>
              <a class="self-center lg:self-start text-base lg:text-lg bg-[#23286b] text-white border-[.1rem] border-[#23286b] rounded-sm text-center w-[8rem] transition-all delay-200 duration-200 hover:bg-transparent hover:text-[#23286b] " href="/product/{item.id}">View More</a>
          </div>
          <div class=" lg:w-[50%]">
              <img src="{mediaurl}{item.banner_image}" alt="">
          </div>
      </div>
    {:else}
       <!-- empty list -->
    {/each}
</div>

<style>
  .carousel-container {
    position: relative;
    margin-top: 6rem;
    overflow-x: hidden;
    background-color: #23286b;
    /* background: linear-gradient(to bottom, #23286b, #4d4fa4); */

  }

  .carousel {
    display: flex;
    width: 100%;
    scroll-snap-type: x mandatory;
    animation: scroll 20s linear infinite;
  }

  .carousel-item {
    position: relative;
    flex: 0 0 20%;
    margin-right: 2rem;
    scroll-snap-align: center;
  }

  .carousel-item:last-child {
    margin-right: 0;
  }

  .product {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 1;
    background-color: rgba(0, 0, 0, 0.5);
    color: white;
    height: 17rem;
    width: 16rem;
    padding: 1rem;
    text-align: center;
  }

  .product h2{
      color: white;
  }
  .product-title {
    margin: 0;
    font-size: 2rem;
  }

  .product-link {
    display: inline-block;
    margin-top: 1rem;
    padding: 0.5rem 1rem;
    border: 1px solid white;
    border-radius: 0.25rem;
    color: white;
    text-decoration: none;
  }

  /* Define the scroll animation for the carousel */
  @keyframes scroll {
    0% {
      transform: translateX(0);
    }
    /* Move the carousel to the left by the width of a single slide */
    33.33% {
      transform: translateX(-50%);
    }
    /* Move the carousel to the left by the width of two slides */
    66.66% {
      transform: translateX(-100%);
    }
    /* Move the first slide to the end of the carousel */
    100% {
      transform: translateX(0);
    }
  }


  .carousel-item:first-child {
    order: 3;
  }

  /* Media Queries */
  @media (max-width: 768px) {
    .carousel-item {
      flex: 0 0 100%;
      margin-right: 0;
    }
    .product-title {
      font-size: 1.5rem;
    }
  }

  @media (min-width: 768px) and (max-width: 992px) {
    .carousel-item {
      flex: 0 0 50%;
      margin-right: 1rem;
    }
    .product-title {
      font-size: 1.75rem;
    }
  }

  @media (min-width: 992px) {
    .carousel-item {
      flex: 0 0 33.33%;
      margin-right: 2rem;
    }
    .product-title {
      font-size: 2rem;
    }
  }
</style>
