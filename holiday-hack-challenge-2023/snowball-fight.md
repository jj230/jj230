---
description: >-
  Tools/Skills: Browser's Developer Tools, HTML, JavaScript, Runtime
  Modifications
---

# Snowball Fight

## SYNOPSIS

Play a snowball fight against Santa and his Elves with another player. If you can, find a way to hack the game to make it a one-player game and/or make it easier to win.

Using Chrome's browser developer tools, I modified the URL to make it a single-player game and changed variables to make it easier to win.

## SOLUTION

1. Clicked on private room
2. Right Clicked → Inspect
3. Clicked Console → selected Room
4. Examined the variables and code
   * [x] `console.log(window);`
   * [x] `console.log(document);`
5.  Modified the URL programmatically

    <mark style="color:green;">`const urlParams = new URLSearchParams(window.location.search);`</mark>

    <mark style="color:green;">`urlParams.set('singlePlayer', 'true');`</mark>

    <mark style="color:green;">``const newUrl = `${window.location.pathname}?${urlParams}`;``</mark>

    <mark style="color:green;">`window.history.replaceState({}, '', newUrl);`</mark>

    <mark style="color:green;">`location.reload();`</mark>&#x20;
6. Re-displayed global variables
   * [x] `console.log(window);`
7. Changed Variables
   * [x] Elfhitboxsize → changed all to 100
   * [x] elfThrowDelay → changed to 200,000
   * [x] Players → health → changed to 50,000
   * [x] Players → throw delay → 0
   * [x] playersVelocity → 2000
   * [x] playersHitBoxSize → all 0s
   * [x] SantaHitBoxSize → all 200s
   * [x] santaThrowDelay → 500,000\


## PROCESS

I initially saw that I would have to pair up with another player, unless I could find a way to hack the game. I’ve never hacked a game, but decided I wanted to learn.

1. The Basics: What is the iframe? Where is the client-side code? How can I find the variables?&#x20;
   *   [x] [**ChatGPT Prompts/Answers**](https://chat.openai.com/share/df7207c3-0c83-45c8-a3c9-87390ddc7d71)

       Example Prompts:&#x20;

       * What is the iframe of a webpage? I would like to right-click on a part of a webpage, then go to the console for that page and change a couple of client-side variables. (I have permission to do this).
       * How do I know what variables exist for that page?
   * [x] Typing into the console is allowed.&#x20;
     * I realized, contrary to my initial assumption, that I needed to type into the console to search for the variables.
2. Updating “Single Player”
   *   [x] &#x20;[**ChatGPT Prompts/Answers**](https://chat.openai.com/share/6ca29cb8-9d2f-4c4e-b2f9-acd6b9957cef)

       &#x20;Example Prompts:&#x20;

       * Is there a way to change these client-side variables so that I can play as a single player? \*included code I found in console\*
       * Based on this code, what would I do to make it so that the game is played in single player mode?
   * [x] Attempts:
     * I then searched through the variables and found something that said “singlePlayer: “false””. I changed it to say “true”. Unfortunately, when I did that and then selected play, I couldn’t see my cursor, move my snowman and no elves or Santa were on the screen.
     * I tried changing the game mode and the single value, but the same thing happened. It looks like there’s something that is set to replace my changes, so maybe I need to look at that.&#x20;
     * I continued using chatgpt to narrow down where I was going wrong. I altered between having it analyze code that looked related to the single player setting and asking for code to help update the game. I ended up going to the javascript directly and updating the local code to say single player, but that wasn’t enough.&#x20;
     * Arriving at the Solution:
       * [x] In the end, I had to update the url itself. All of my searches can be seen in the following link.
3. Further Exploration
   * What more can I do?
     * [x] Updated variables such as speed and the size of the hit box. I managed to give myself a lot of health and made it so the elves and santa couldn’t throw snowballs. BUT I accidentally made it so that Santa couldn’t be damaged
       *   [x] Problem Identified: I thought of “hitbox” as the opposite of what they are.I thought playerhitbox, for instance, was about how effective the player would be when they attacked someone. But, it turns out, it’s about when they will get damaged.

           [**ChatGPT Prompts/Answers**](https://chat.openai.com/share/7090e80a-ef8a-4890-aaaf-5834ecc3858b)

           Prompts:&#x20;

           * What does hitboxsize refer to in the context of computer game code?
           * So, if the box is too small, that would make the object hard to ever hit?
       * [x] Problem Solved: I then changed my hitbox to zero, so that I could not ever be damaged. And increased the numbers of the elves and santa and they became easy targets.
