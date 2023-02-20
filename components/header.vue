<template>
  <nav>
    <ul>
      <li>Flashar</li>
<!--      <li><input placeholder="search"></li>
      <li>
        <NuxtLink to="/">Go to Home</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/searchresults">Go to Search Results</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/flashcardlisting">Go to Flashcard Listing</NuxtLink>
      </li>-->
    </ul>
  </nav>
</template>

<style>
nav ul li {
  display: flex;
  margin-left: 40px;
}

nav ul li:first-child {
  margin-left: 700px;
  color: white;
}

input {
  height: 80%;
  align-self: center;
  border: orange 2px solid;
}

nav ul {
  margin: 0;
  padding-top: 25px;
  padding-bottom: 50px;
  display: flex;
  align-content: center;
}

nav {
  font-size: 36px;
  font-weight: bold;
  padding-left: 0;
  /*background-color: #bfe2fa;*/
  margin: 0;
}

</style>