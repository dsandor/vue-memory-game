# vue-memory-game

> Classic memory matching game in Vue.js

## Build Setup - Just run the final code.

``` bash
# install dependencies
yarn install

# serve with hot reload at localhost:8080
yarn dev

# build for production with minification
yarn build

# build for production and view the bundle analyzer report
yarn build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

---

## Workshop Instructions

Simple Vue.js application for the ATL Vue.js meetup.  In this workshop we are going to build a "memory" game.

### Install all workshop prerequisites.

Please be sure that all of these prerequisites are installed before continuing.

#### Install NodeJS
**NodeJS**
Please be sure you have NodeJS v8+ installed.

**MAC OSX**

If you need to install NodeJS please install nvm here:
[https://github.com/creationix/nvm#install-script](https://github.com/creationix/nvm#install-script)

Then install NodeJS with the command:

```
nvm install v8
nvm alias default v8
```

**Windows users please install from here:**

[https://nodejs.org/en/download](https://nodejs.org/en/download)

#### Install required NodeJS packages.

**Install yarn package manager & Vue CLI**

```
npm i yarn vue-cli -g
```

--


### Game Logic

The board will contain 30 tiles and will be laid out on a 640 x 496 pixel game board.  The player can click a tile to reveal a word on the tile. The player needs to match pairs of words.  If a player clicks two tiles and they do not match the tiles must stay visible for 1 second and then disappear.  When a match is made, the words stay visible and the pair is given a unique colored border.

![Completed Game Board](https://raw.githubusercontent.com/dsandor/vue-memory-game/master/docs/img/example-game-board.png)


### Create the project using the vue command line.

For the purposes of this documentation I am going to assume the project will be created in a folder `/Projects` we are going to use the Vue command line utility in order to bootstrap a webpack based vue template that we will work from.  We will name this project `vue-memory-game` so the files for this project will be in `~/Project/vue-memory-game`.


```
cd ~/Projects
vue init webpack vue-memory-game
```

The Vue CLI will ask you a few questions.  Please choose the same answers for the purposes of this documentation so that we are all on the same page.

|Question|Answer|
|---|---|
Project name|`vue-memory-game`
Project description|`Classic memory matching game in Vue.js`
Author|`your email address`
Vue build|`standalone`
Install vue-router?|`No`
Use ESLint to lint your code?|`Yes`
Pick an ESLint preset|`Airbnb`
Set up unit tests|`No`
Setup e2e tests with Nightwatch?|`No`
Should we run `npm install` for you after the project has been created?|`yarn`

Now change into the project directory and start the dev server:

```
cd vue-memory-game
yarn dev
```

If all goes well you will have a basic VueJS template up and running and you can navigate to this web page here: [http://localhost:8080](http://localhost:8080)

## Coding Steps

Here is a quick cheat for creating a vue component.  Below is the absolute minimum we will start with, you can copy and paste this code snippet in when creating a new vue component and then just start filling in the sections you need.

**Empty.vue**

```
<template>
  <div class="">
  </div>
</template>

<script>
export default {
  name: '',
  data() {
    return {
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
```

**GameTile.vue**

We are going to start with our most basic component, the GameTile.  This is going to be a little square on the game board that displays a word or a number to the user.  There will be 30 of these on the game board.

Create a new file under `src/Components` and name it `GameTile.vue`.  Copy and paste that empty template above to make this easier.

Fill out the style section with the style we want to use for the tile.

```
<style scoped>
.game-tile-content {
  color: white;
  display: inline-block;
  width: 60px;
  height: 60px;
  margin: 16px;
  background: magenta;
  border-width: 2px;
}
</style>
```

Next, we will fill out the script.  Here we name the component `GameTile` and tell the component that we are going to take a property named `tileConten`. We are using local state to store the visibility of the tile.  Finally, when the tile is clicked we will display an alert to the user telling them what tile they clicked on.


```
<script>
export default {
  name: 'GameTile',
  props: ['tileContent'],
  data() {
    return {
      isContentVisible: false,
    };
  },
  methods: {
    clickedTile() {
      // eslint-disable-next-line
      alert(`clicked tile: ${this.tileContent}`);
    },
  },
};
</script>
```

Finally, we will create the HTML for the tile.  This is quite simple as you can see below.

```
<template>
  <p class="game-tile-content" @click="clickedTile">{{ tileContent }}</p>
</template>
```

**GameBoard.vue**

This will be our main game board component.  It will be the page that contains the game board and the board will contain all the tiles.

Start by creating a template.  Here we just need a boart containter div and enumerate all of our tiles.

```
<template>
  <div class="game-board">
    <GameTile v-for="tile in tiles" :key="tile" :tileContent="tile" />
  </div>
</template>
```

Next, we need some code to create those tiles we referenced above.  This script will reference a GameTile component that will actually represent the game tile.  We name our component and create some tiles that we will display.

```
<script>
import GameTile from './GameTile';

export default {
  name: 'GameBoard',
  components: {
    GameTile,
  },
  data() {
    return {
      tiles: [
        1, 2, 3, 4, 5, 6, 7, 8, 9,
        10, 11, 12, 13, 14, 15, 16,
        17, 18, 19, 20, 21, 22, 23,
        24, 25, 26, 27, 28, 29, 30],
    };
  },
};
</script>
```

Finally, we are going to style the game board so it does not look so dull.

```
<style scoped>
.game-board {
  background: grey;
  height: 100%;
  text-align: center;
  margin: 0 auto;
  height: 495px;
  width: 640px;
}
</style>
```
