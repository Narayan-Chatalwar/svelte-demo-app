<script>
  import "../Styles/main.css";
  import "resize-observer-polyfill";

  import { onMount } from "svelte";

  let maindata = null;

  const targetURL = "http://localhost:8080/maindata";
  // "https://main--mywebsite--narayan-chatalwar.hlx.live/dataforindex.json";

  const getMainData = async () => {
    try {
      const res = await fetch(targetURL);
      const data = await res.json();
      maindata = data.data;
    } catch (err) {
      console.log(err, "error in getting main data");
    }
  };

  let videoIframe;

  const replayVideo = () => {
    if (videoIframe) {
      videoIframe.play();
    }
  };

  onMount(() => {
    getMainData();

    videoIframe = document.getElementById("video-iframe");

    videoIframe.addEventListener("ended", replayVideo);

    if (videoIframe) {
      videoIframe.play();
    }
  });
</script>

<div>
  {#if maindata}
    <div class="flex pt-[200px] pb-24 px-12 bg-[#f0ede8] gap-x-32">
      <div class="flex flex-col gap-[20px]">
        <p class="font-black text-[59px] leading-[66px] tracking-[4px]">
          {maindata[0].title}
        </p>
        <p class="font-light text-[26.3px]">{maindata[0].description}</p>
      </div>
      <div>
        <iframe
          title="herovideo"
          id="video-iframe"
          src={`${maindata[0].medialink}&autoplay=1&muted=1`}
          width="640"
          height="360"
          frameborder="0"
          allowfullscreen
          allow="autoplay"
        />
      </div>
    </div>
  {/if}

  {#if maindata}
    <div class="flex gap-[60px] py-24 px-12">
      <div>
        <img src={maindata[1].medialink} class="w-full" alt="section1" />
      </div>
      <div class="flex flex-col gap-[16px] justify-center max-w-[607px]">
        <p class="max-w-[492px] text-[29.8px] font-bold">{maindata[1].title}</p>
        <p class="text-[19.4px]">{maindata[1].description}</p>
        <div>
          <button
            class="bg-[#f9de3b] text-[18px] font-medium py-4 px-12 rounded-[300px]"
            >{maindata[1].button}</button
          >
        </div>
      </div>
    </div>
  {/if}

  {#if maindata}
    <div class="flex flex-row-reverse gap-[60px] py-24 px-12">
      <div>
        <img src={maindata[2].medialink} class="w-full" alt="section1" />
      </div>
      <div class="flex flex-col gap-[16px] justify-center max-w-[607px]">
        <p class="max-w-[492px] text-[29.8px] font-bold">{maindata[2].title}</p>
        <p class="text-[19.4px]">{maindata[2].description}</p>
        <div>
          <button
            class="bg-[#f9de3b] text-[18px] font-medium py-4 px-12 rounded-[300px]"
            >{maindata[2].button}</button
          >
        </div>
      </div>
    </div>
  {/if}

  {#if maindata}
    <div class="bg-[#f0ede8] py-[70px]">
      <div
        class="flex flex-col justify-center items-center max-w-[883px] m-auto gap-[16px]"
      >
        <p class="text-[59px] font-bold">{maindata[3].title}</p>
        <p class="text-[19px] text-center leading-[33px]">
          {maindata[3].description}
        </p>
        <div>
          <button
            class="bg-[#000000] text-[#ffffff] text-[18px] rounded-[300px] font-medium py-4 px-12"
            >{maindata[3].button}</button
          >
        </div>
      </div>
    </div>
  {/if}
</div>
