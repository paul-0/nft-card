<template>
  <CardComponent />
</template>

<script>
import CardComponent from "@/components/CardComponent";
export default {
  name: 'App',
  components: {CardComponent}
}
</script>

<style>
@import url(https://fonts.googleapis.com/css2?family=Barlow+Semi+Condensed:ital,wght@0,400;0,500;0,700;0,900;1,500&family=Fredoka:wght@400;500;600&display=swap);

:root {
  --soft-blue: hsl(215, 51%, 70%);
  --cyan: hsl(178, 100%, 50%);

  --very-dark-blue: hsl(217, 54%, 11%);
  --dark-blue: hsl(216, 50%, 16%);
  --blue: hsl(215, 32%, 27%);
  --white: hsl(0, 0%, 100%);
}

html, body, #app {
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
}

#app {
  font-family: "Barlow Semi Condensed", sans-serif;
  background-color: var(--very-dark-blue);
  display: flex;
  align-items: center;
  justify-content: center;
}

p {
  font-size: 18px;
}
</style>
