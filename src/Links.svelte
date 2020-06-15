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
  .next,
  .prev {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 50px;
    height: 50px;
  }

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
  <div on:click={showPrev} id="prevBtn" class="prev">
    <i class="fas fa-chevron-left" />
  </div>

  <a href="{links[image]}.com">
    <img class="img" src="{links[image]}.svg" alt="" />
  </a>

  <div on:click={showNext} id="nextBtn" class="next">
    <i class="fas fa-chevron-right" />
  </div>

</div>
