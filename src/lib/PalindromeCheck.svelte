<script lang="ts">
  import { each } from "svelte/internal";

  let palindrome: string = "";

  let onlyLetters = true;

  $: palindromeText = onlyLetters
    ? [...palindrome].filter((char) => /^[a-zA-Z]*$/.test(char)).join("")
    : palindrome;

  $: palindromeTextCapitalized = palindromeText.toLocaleUpperCase();

  $: onlyHasAlphabet = /^[a-zA-Z]*$/.test(palindrome);

  $: palindromeReversed = [...palindromeText].reverse().join("");

  $: isPalindrome =
    palindromeText.toLocaleLowerCase() ===
    palindromeReversed.toLocaleLowerCase();

  $: characterMatchIndicator = [...palindromeTextCapitalized].map(
    (c, index) =>
      c ===
      palindromeTextCapitalized[palindromeTextCapitalized.length - index - 1]
  );
</script>

<div>
  <input
    type="text"
    name="palindrome"
    id="palindrome"
    bind:value={palindrome}
    placeholder="Check your palindrome here!"
  />
  {#if !onlyHasAlphabet && onlyLetters}
    <p class="error">Try to only use letters and spaces</p>
  {/if}

  {#if palindromeText.length === 0}
    <p class="text-faded">Enter a word. Well tell you if it's a palindrome!</p>
  {:else}
    <p class:text-faded={palindromeText.length === 0} class="input-display">
      {palindromeText.toLocaleUpperCase() || ""}
    </p>
  {/if}

  <p class="input-display">
    {#each palindromeReversed.toLocaleUpperCase() as character, index}
      <span
        class:error={!characterMatchIndicator[index]}
        class:is-not-palindrome={!characterMatchIndicator[index]}
        class:is-palindrome={characterMatchIndicator[index]}>{character}</span
      >
    {/each}
  </p>

  {#if palindromeText.length > 0}
    <p
      class:is-palindrome={isPalindrome}
      class:error={!isPalindrome}
      class:result-text={true}
    >
      {isPalindrome
        ? "Yeah, it's a palindrome!"
        : "Nope, it's not the same backwards"}
    </p>
  {/if}

  <input
    type="checkbox"
    name="only-letters"
    id="only-letters"
    bind:checked={onlyLetters}
  />
  <label for="only-letters"> Ignore non-letters </label>
</div>

<style>
  input[type="text"] {
    width: 30ch;
    padding-top: 0.5em;
    padding-bottom: 0.5em;
    padding-left: 0.5em;
    padding-right: 0.5em;
    font-size: 1.25em;
  }

  .result-text {
    font-size: 2em;
  }

  .input-display {
    font-family: monospace;
    font-size: 1.5em;
  }

  .is-palindrome {
    color: #008800;
  }

  .error {
    color: #b00202;
  }

  .is-not-palindrome {
    background-color: #ffaaaa;
  }

  .text-faded {
    color: #00000088;
  }
</style>
