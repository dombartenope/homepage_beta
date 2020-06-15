<script>
  let image = 0;
  const links = ["google", "youtube", "reddit"];

  const showPrev = () => {
    image--;
    if (image < 0) {
      image = links.length - 1;
    }
  };
  const showNext = () => {
    image++;
    if (image > links.length - 1) {
      image = 0;
    }
  };
</script>

<style>
  .imgContainer {
    display: flex;
    align-items: center;
    justify-content: space-around;
    width: 100%;
    overflow: hidden;
  }

  .img {
    width: 150px;
    height: 150px;
    filter: grayscale();
    padding: 20px;
    transition: transform 0.2s ease-in-out;
  }
  .img:active {
    filter: none;
  }
</style>

<div class="imgContainer">

  <i on:click={showPrev} id="prevBtn" class="fas fa-chevron-left" />

  <a href="{links[image]}.com">
    <img class="img" src="{links[image]}.svg" alt="" />
  </a>

  <i on:click={showNext} id="nextBtn" class="fas fa-chevron-right" />

</div>
