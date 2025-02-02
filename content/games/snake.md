---
title: "Snake Game"
date: 2025-02-02
draft: false
---

<script>
  var canvas, ctx, keystate, frames, player, score;
  function main() {
    canvas = document.createElement("canvas");
    canvas.width = 400;
    canvas.height = 400;
    document.body.appendChild(canvas);
    ctx = canvas.getContext("2d");

    frames = 0;
    keystate = {};
    document.addEventListener("keydown", function(evt) {
      keystate[evt.key] = true;
    });
    document.addEventListener("keyup", function(evt) {
      delete keystate[evt.key];
    });

    init();
    loop();
  }

  function init() {
    score = 0;
    player = { x: 10, y: 10, dx: 1, dy: 0 };
    food = { x: 15, y: 15 };
  }

  function loop() {
    update();
    draw();
    frames++;
    requestAnimationFrame(loop);
  }

  function update() {
    if (keystate["ArrowLeft"]) { player.dx = -1; player.dy = 0; }
    if (keystate["ArrowRight"]) { player.dx = 1; player.dy = 0; }
    if (keystate["ArrowUp"]) { player.dx = 0; player.dy = -1; }
    if (keystate["ArrowDown"]) { player.dx = 0; player.dy = 1; }

    player.x += player.dx;
    player.y += player.dy;
  }

  function draw() {
    ctx.fillStyle = "black";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ctx.fillStyle = "lime";
    ctx.fillRect(player.x * 20, player.y * 20, 20, 20);

    ctx.fillStyle = "red";
    ctx.fillRect(food.x * 20, food.y * 20, 20, 20);
  }

  window.onload = main;
</script>

<p>Gioca a Snake! Usa le frecce per muoverti.</p>
