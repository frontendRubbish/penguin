<script lang="ts">
  import { onMount } from 'svelte';

  const classes = ['', 'inner--dark', 'inner--light'];

  let confetti = new Array(100).fill(undefined)
    .map((_, i) => {
        return {
            x: Math.random() * 100,
            y: -20 - Math.random() * 80,
            rotInner: getRandomInt(360),
            r: 0.1 + Math.random() * 1,
            rotX: getRandomInt(360),
            rotY: getRandomInt(360),
            tiltPos: getRandomInt(360),
            tilt: Math.random() * 0.1,
            class: classes[getRandomInt(3)]
        };
    })
    .sort((a, b) => a.r - b.r);

  function getRandomInt(max: number) {
    return Math.floor(Math.random() * Math.floor(max));
  }

  function startConfetti() {
    let frame: number;
    let continueAnimation = true;

    function loop() {
      if (continueAnimation) {
        frame = requestAnimationFrame(loop);
      }

      let outCounter = 0;

      confetti = confetti.map(emoji => {
        const way = Math.abs(emoji.y - 680);
        let acc = way / 2 * 0.05;
        if ( acc < 10) {
            acc = 7;
        }
        /* let acc = way / 2 * 0.1;
        if ( acc < 10) {
            acc = 10;
        }
        let acc = way / 2 * 0.01;
        if ( acc < 4) {
            acc = 4;
        } */
        emoji.rotX ++;
        emoji.rotY += 50;
        emoji.y += acc * emoji.r;
        emoji.tiltPos += 10;

        if (emoji.y > 800) {
            outCounter ++;
        }

        if (outCounter === 100) {
            continueAnimation = false;
        }

        return emoji;
      });
    }

    loop();

    return () => cancelAnimationFrame(frame);
  }

  onMount(() => {
    setTimeout( () => startConfetti(), 400);
  });
</script>

<style lang="postcss">
  .confetti {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 999;
  }
  .outer {
    position: absolute;
  }
  .inner {
    position: absolute;
    display: block;
    width: 20px;
    height: 20px;
    background-color: theme(colors.blue.500);
  }

  .inner--dark {
    background-color: theme(colors.blue.500);
  }
  .inner--light {
    background-color: theme(colors.blue.200);
  }
</style>

<div class="confetti">
  {#each confetti as c}
    <div class="outer" style="left: {c.x}%; top: {c.y}px;transform: rotateY({c.rotX}deg)">
      <span class="inner {c.class}" style="transform: translateX({c.tiltPos * c.tilt}px) scale({c.r}) rotate({c.rotInner}deg)"></span>
    </div>
  {/each}
</div>