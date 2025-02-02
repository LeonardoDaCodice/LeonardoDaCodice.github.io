---
title: "Snake Game"
date: 2025-02-02
draft: false
---

<p>Gioca a Snake! Usa le frecce per muoverti.</p>

<canvas id="gameCanvas" width="400" height="400" style="border:1px solid black;"></canvas>

<script>
document.addEventListener("DOMContentLoaded", function() {
    var canvas = document.getElementById("gameCanvas");
    var ctx = canvas.getContext("2d");

    var gridSize = 20;
    var snake = [{ x: 10, y: 10 }];
    var food = { x: 15, y: 15 };
    var direction = "RIGHT";

    function update() {
        var head = Object.assign({}, snake[0]);

        if (direction === "RIGHT") head.x++;
        if (direction === "LEFT") head.x--;
        if (direction === "UP") head.y--;
        if (direction === "DOWN") head.y++;

        if (head.x === food.x && head.y === food.y) {
            food.x = Math.floor(Math.random() * (canvas.width / gridSize));
            food.y = Math.floor(Math.random() * (canvas.height / gridSize));
        } else {
            snake.pop();
        }

        snake.unshift(head);
    }

    function draw() {
        ctx.fillStyle = "black";
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        ctx.fillStyle = "lime";
        snake.forEach(part => {
            ctx.fillRect(part.x * gridSize, part.y * gridSize, gridSize, gridSize);
        });

        ctx.fillStyle = "red";
        ctx.fillRect(food.x * gridSize, food.y * gridSize, gridSize, gridSize);
    }

    function loop() {
        update();
        draw();
        setTimeout(loop, 100);
    }

    document.addEventListener("keydown", function(event) {
        if (event.key === "ArrowRight" && direction !== "LEFT") direction = "RIGHT";
        if (event.key === "ArrowLeft" && direction !== "RIGHT") direction = "LEFT";
        if (event.key === "ArrowUp" && direction !== "DOWN") direction = "UP";
        if (event.key === "ArrowDown" && direction !== "UP") direction = "DOWN";
    });

    loop();
});
</script>
