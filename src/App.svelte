<script lang="ts">
import PalindromeCheck from "./lib/PalindromeCheck.svelte";
</script>

<main>
  <a id="repoLink" href="https://github.com/DeltaHarbinger/prime-checker">
    <img id="githubImage" src="https://upload.wikimedia.org/wikipedia/commons/9/91/Octicons-mark-github.svg" alt="github-logo">
  </a>
  <h3>Palindrome Checker</h3>
  <PalindromeCheck />
  <footer>
    <a href="http://github.com/DeltaHarbinger">
      © DeltaHarbinger
    </a>
  </footer>
</main>

<style>
h3 {
  text-transform: uppercase;
  margin: 2rem auto;
  max-width: 14rem;
}

h3 {
  font-size: 2rem;
  font-weight: 500;
  line-height: 1.1;
}

#githubImage {
  height: 4em;
}

#repoLink {
  position: absolute;
  bottom: 2em;
  right: 2em;
}

footer {
  padding-top: .5em;
  padding-bottom: .5em;
  position: absolute;
  width: 100%;
  bottom: 0;
  left: 0;
  font-size: 1.25em;
}

a {
  text-decoration: none;
  color: black;
}

@media only screen and (min-width: 820px) {
  footer {
    text-align: left;
  }

  a {
    padding-left: 2em;
  }
}
</style>