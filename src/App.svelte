<script>
  let loading = true;
  let category = "Any";
  let categories = [];
  let jokes = [];
  let joke_index = -1;
  import { onMount } from "svelte";

  onMount(() => {
    fetchCategory();
    fetchJoke();
  });
  function fetchCategory() {
    loading = true;
    fetch("https://jokeapi.p.rapidapi.com/categories?format=json", {
      method: "GET",
      headers: {
        "x-rapidapi-host": "jokeapi.p.rapidapi.com",
        "x-rapidapi-key": "bb640b1d62msh3f6b06f572a14abp18f020jsn38055ecb3aae",
      },
    })
      .then((response) => response.json())
      .then((response) => {
        categories = response.categories;
        loading = false;
      })
      .catch((err) => {
        alert(err);
      });
  }
  function fetchJoke() {
    loading = true;
    fetch(
      "https://jokeapi.p.rapidapi.com/category/" + category + "?format=json",
      {
        method: "GET",
        headers: {
          "x-rapidapi-host": "jokeapi.p.rapidapi.com",
          "x-rapidapi-key":
            "bb640b1d62msh3f6b06f572a14abp18f020jsn38055ecb3aae",
        },
      }
    )
      .then((response) => response.json())

      .then((response) => {
        jokes = [...jokes, response];
        loading = false;
        joke_index++;
        category = jokes[joke_index].category;
      })
      .catch((err) => {
        alert(err);
      });
  }
  function handlePrev() {
    joke_index--;
    category = jokes[joke_index].category;
  }
  function handleNext() {
    if (joke_index < jokes.length - 1) {
      joke_index++;
      category = jokes[joke_index].category;
    } else {
      fetchJoke();
    }
  }
  function setCategory(c) {
    category = c;
    fetchJoke();
    joke_index = jokes.length - 1;
  }
</script>

<style>
  * {
    font-family: "Open Sans", -apple-system, BlinkMacSystemFont, "Segoe UI",
      Roboto, Oxygen, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
  }
  :global(html) {
    margin: 0;
    padding: 0;
  }

  @media (min-width: 320px) {
    /* smartphones, iPhone, portrait 480x320 phones */
    :global(body) {
      background: #171824;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      margin: 0;
      padding: 10px;
      width: 100%;
      height: 100%;
      box-sizing: border-box;
    }
    .joke-container {
      width: 90%;
      max-width: 700px;
    }
    .joke-header {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 20px;
    }
    .joke-title {
      color: #f02222;
      font-size: 20px;
      font-weight: 800;
      padding: 0;
      margin: 0;
    }
    .joke-button-prev {
      cursor: pointer;
      background: #2d2e3d;
      padding: 4px 8px;
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 9px;
      font-weight: 800;
      margin-right: 5px;
    }
    .joke-button-prev:active,
    .joke-button-prev:hover {
      background: #262633;
    }

    .joke-button-next {
      cursor: pointer;
      background: #f02222;
      padding: 4px 8px;
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 9px;
      font-weight: 800;
    }
    .joke-button-next:active,
    .joke-button-next:hover {
      background: #c01717;
    }
    .joke-box {
      background: #212230;
      border: 3px solid #2d2e3d;
      box-shadow: 0px 5px 30px rgba(0, 0, 0, 0.25);
      width: 100%;
      border-radius: 10px;
      margin-bottom: 20px;
      padding: 15px;
      box-sizing: border-box;
    }
    .joke-text {
      text-align: center;
      letter-spacing: 2px;
      color: #c7c7c7;
      font-size: 16px;
      font-weight: 200;
    }
    .joke-category-container {
      width: 100%;
      display: flex;
      justify-content: space-around;
      align-items: center;
    }
    .joke-category {
      cursor: pointer;
      width: 100%;
      padding: 4px;
      background: #11121e;
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 6px;
      font-size: 9px;
      font-weight: 700;
      color: #212230;
      text-align: center;
      margin: 3px;
    }
    .joke-category-active {
      cursor: pointer;
      width: 100%;
      padding: 4px;
      background: #15eb51;
      border-radius: 6px;
      font-size: 9px;
      font-weight: 700;
      color: rgba(0, 0, 0, 0.5);
      box-shadow: 0px 0px 10px 5px rgba(21, 235, 81, 0.25);
      text-align: center;
      margin: 3px;
    }
    .joke-category:active,
    .joke-category:hover {
      color: #fff;
    }
  }

  @media (min-width: 481px) {
    /* portrait e-readers (Nook/Kindle), smaller tablets @ 600 or @ 640 wide. */
    :global(body) {
      background: #171824;
      display: flex;
      justify-content: center;
      align-items: center;
      margin: 0;
      padding: 10px;
      width: 100%;
      height: 100%;
      box-sizing: border-box;
    }
    .joke-container {
      width: 80%;
      max-width: 700px;
    }
    .joke-header {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 20px;
    }
    .joke-title {
      color: #f02222;
      font-size: 40px;
      font-weight: 800;
      padding: 0;
      margin: 0;
    }
    .joke-button-prev {
      cursor: pointer;
      background: #2d2e3d;
      padding: 10px 20px;
      color: #fff;
      border: none;
      border-radius: 12px;
      font-size: 18px;
      font-weight: 800;
      margin-right: 10px;
    }
    .joke-button-prev:active,
    .joke-button-prev:hover {
      background: #262633;
    }

    .joke-button-next {
      cursor: pointer;
      background: #f02222;
      padding: 10px 20px;
      color: #fff;
      border: none;
      border-radius: 12px;
      font-size: 18px;
      font-weight: 800;
    }
    .joke-button-next:active,
    .joke-button-next:hover {
      background: #c01717;
    }
    .joke-box {
      background: #212230;
      border: 3px solid #2d2e3d;
      box-shadow: 0px 5px 30px rgba(0, 0, 0, 0.25);
      width: 100%;
      border-radius: 25px;
      margin-bottom: 20px;
      padding: 40px;
      box-sizing: border-box;
    }
    .joke-text {
      text-align: center;
      letter-spacing: 2px;
      color: #c7c7c7;
      font-size: 20px;
      font-weight: 200;
    }
    .joke-category-container {
      width: 100%;
      display: flex;
      justify-content: space-around;
      align-items: center;
    }
    .joke-category {
      cursor: pointer;
      width: 100%;
      padding: 4px;
      background: #11121e;
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 12px;
      font-size: 16px;
      font-weight: 700;
      color: #212230;
      text-align: center;
      margin: 5px;
    }
    .joke-category-active {
      cursor: pointer;
      width: 100%;
      padding: 4px;
      background: #15eb51;
      border-radius: 12px;
      font-size: 16px;
      font-weight: 700;
      color: rgba(0, 0, 0, 0.5);
      box-shadow: 0px 0px 10px 5px rgba(21, 235, 81, 0.25);
      text-align: center;
      margin: 5px;
    }
    .joke-category:active,
    .joke-category:hover {
      color: #fff;
    }
  }
</style>

<div class="joke-container">
  <div class="joke-header">
    <div>
      <h5 class="joke-title">Daily Jokes</h5>
    </div>

    <div>
      {#if joke_index > 0}
        <button class="joke-button-prev" on:click={handlePrev}>Previous</button>
      {/if}
      <button class="joke-button-next" on:click={handleNext}>Next Jokes</button>
    </div>
  </div>
  <div class="joke-box">
    {#if loading || jokes.length === 0}
      <p class="joke-text">Please wait...</p>
    {:else if jokes[joke_index].type === 'single'}
      <p class="joke-text">{jokes[joke_index].joke}</p>
    {:else}
      <p class="joke-text">
        {jokes[joke_index].setup}&nbsp;{jokes[joke_index].delivery}
      </p>
    {/if}
  </div>
  <div class="joke-category-container">
    {#each categories as c, i}
      <div
        class={c === category ? 'joke-category-active' : 'joke-category'}
        on:click={() => setCategory(c)}>
        #{c}
      </div>
    {/each}
  </div>
</div>
