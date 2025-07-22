<script>
  // import LeftAlignedExample from "./sections/LeftAlignedExample.svelte";
  // import RightAlignedExample from "./sections/RightAlignedExample.svelte";
  // import ImageExample from "./sections/ImageExample.svelte";

  // import Scroll3_Graph2 from "./sections/Scroll3_Graph2.svelte";
  // import Scroll4_Graph3 from "./sections/Scroll4_Graph3.svelte";
  // import Scroll5_Graph4 from "./sections/Scroll5_Graph4.svelte";
  // import Data1 from "./sections/data1.svelte";
  // import Data2 from "./sections/data2.svelte";

  import TitleSection from "./sections/TitleSection.svelte";
  import Scroll_1TV from "./sections/Scroll1_TV.svelte";
  import Scroll2_Graph1 from "./sections/Scroll2_Graph1.svelte";
  import Section1 from "./sections/Section1.svelte";
  import Section2 from "./sections/Section2.svelte";
  import DataTest from "./sections/data_test.svelte";
  import Closing from "./sections/Closing.svelte";
</script>

<main>
  <!--Hook-->
  <TitleSection />
  <Section1  />
  <Section2  />
  
  <!--Bowie-->
  <Scroll_1TV />

  <!--Mortality Rate-->
  <Scroll2_Graph1 />
  
  <!--BWDC 1: available care-->
  <!--BWDC 2: location & insurances barriers-->
  <!--BWDC 3: disproportionate harm-->
  <DataTest/>

  <Closing /> 

</main>
