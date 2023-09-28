<script>
  import "../Styles/footer.css";
  import { onMount } from "svelte";

  let maindata = null;
  let footerdata = null;

  const targetmainURL = "https://proxyserver-seven.vercel.app/maindata";
  // "http://localhost:8080/maindata";
  // "https://main--mywebsite--narayan-chatalwar.hlx.live/dataforindex.json";

  const targetfooterURL = "https://proxyserver-seven.vercel.app/footerdata";
  // "http://localhost:8080/footerdata";
  // "https://main--mywebsite--narayan-chatalwar.hlx.live/dataforfooter.json";

  const getMainData = async () => {
    try {
      const res = await fetch(targetmainURL);
      const data = await res.json();
      maindata = data.data;
    } catch (err) {}
  };

  const getFooterData = async () => {
    try {
      const res = await fetch(
        // corsAnywhereURL +
        targetfooterURL
      );
      const data = await res.json();
      footerdata = data.data;
    } catch (err) {}
  };

  const leftfootertags = () => {
    return footerdata ? footerdata.filter((item) => item.id > 12) : [];
  };

  const rightfootertags = () => {
    return footerdata ? footerdata.filter((item) => item.id <= 12) : [];
  };

  onMount(async () => {
    // Use Promise.all to coordinate both fetch operations
    await Promise.all([getMainData(), getFooterData()]);
  });
</script>

<div>
  {#if maindata}
    <div class="flex flex-col sm:flex-row justify-between p-[50px]">
      <div>
        <p class="text-[22px] font-bold mb-2.5">{maindata[4].title}</p>
        <p>{maindata[4].description}</p>
        <div class="footerleftcontent">
          {#each leftfootertags() as item (item.id)}
            <span>{item.title} &nbsp; | &nbsp;</span>
          {/each}
        </div>
      </div>
      <div class="footerleftcontent">
        {#each rightfootertags() as item (item.id)}
          <span>{item.title} &nbsp;</span>
        {/each}
      </div>
    </div>
  {/if}
</div>
