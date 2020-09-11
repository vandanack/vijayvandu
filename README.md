<!DOCTYPE html>
<html>
<head>
	<title>Birthday</title>
	<meta name="viewport" content="width=device-width",initial-sacle=1.0>
	<script type="text/javascript">
		"use strict";

let canvas, width, height, ctx;
let fireworks = [];
let particles = [];

function setup() {
	canvas = document.getElementById("canvas");
	setSize(canvas);
	ctx = canvas.getContext("2d");
	ctx.fillStyle = "#000000";
	ctx.fillRect(0, 0, width, height);
	fireworks.push(new Firework(Math.random()*(width-200)+100));
	window.addEventListener("resize",windowResized);
	document.addEventListener("click",onClick);
}

setTimeout(setup,1);

function loop(){
	ctx.globalAlpha = 0.1;
	ctx.fillStyle = "#000000";
	ctx.fillRect(0, 0, width, height);
	ctx.globalAlpha = 1;

	for(let i=0; i<fireworks.length; i++){
		let done = fireworks[i].update();
		fireworks[i].draw();
		if(done) fireworks.splice(i, 1);
	}

	for(let i=0; i<particles.length; i++){
		particles[i].update();
		particles[i].draw();
		if(particles[i].lifetime>80) particles.splice(i,1);
	}

	if(Math.random()<1/60) fireworks.push(new Firework(Math.random()*(width-200)+100));
}
setInterval(loop, 1/60);
//setInterval(loop, 100/60);
class Particle{
	constructor(x, y, col){
		this.x = x;
		this.y = y;
		this.col = col;
		this.vel = randomVec(2);
		this.lifetime = 0;
	}

	update(){
		this.x += this.vel.x;
		this.y += this.vel.y;
		this.vel.y += 0.02;
		this.vel.x *= 0.99;
		this.vel.y *= 0.99;
		this.lifetime++;
	}

	draw(){
		ctx.globalAlpha = Math.max(1-this.lifetime/80, 0);
		ctx.fillStyle = this.col;
		ctx.fillRect(this.x, this.y, 2, 2);
	}
}

class Firework{
	constructor(x){
		this.x = x;
		this.y = height;
		this.isBlown = false;
		this.col = randomCol();
	}

	update(){
		this.y -= 3;
		if(this.y < 350-Math.sqrt(Math.random()*500)*40){
			this.isBlown = true;
			for(let i=0; i<60; i++){
				particles.push(new Particle(this.x, this.y, this.col))
			}
		}
		return this.isBlown;
	}

	draw(){
		ctx.globalAlpha = 1;
		ctx.fillStyle = this.col;
		ctx.fillRect(this.x, this.y, 2, 2);
	}
}

function randomCol(){
	var letter = '0123456789ABCDEF';
	var nums = [];

	for(var i=0; i<3; i++){
		nums[i] = Math.floor(Math.random()*256);
	}

	let brightest = 0;
	for(var i=0; i<3; i++){
		if(brightest<nums[i]) brightest = nums[i];
	}

	brightest /=255;
	for(var i=0; i<3; i++){
		nums[i] /= brightest;
	}

	let color = "#";
	for(var i=0; i<3; i++){
		color += letter[Math.floor(nums[i]/16)];
		color += letter[Math.floor(nums[i]%16)];
	}
	return color;
}

function randomVec(max){
	let dir = Math.random()*Math.PI*2;
	let spd = Math.random()*max;
	return{x: Math.cos(dir)*spd, y: Math.sin(dir)*spd};
}

function setSize(canv){
	canv.style.width = (innerWidth) + "px";
	canv.style.height = (innerHeight) + "px";
	width = innerWidth;
	height = innerHeight;

	canv.width = innerWidth*window.devicePixelRatio;
	canv.height = innerHeight*window.devicePixelRatio;
	canvas.getContext("2d").scale(window.devicePixelRatio, window.devicePixelRatio);
}

function onClick(e){
	fireworks.push(new Firework(e.clientX));
}

function windowResized(){
	setSize(canvas);
	ctx.fillStyle = "#000000";
	ctx.fillRect(0, 0, width, height);
}
	</script>
	<style type="text/css">
		@import url('htpps://fonts.googleapis.com/css?family=Bad+Script');

		nav {
			margin: 0;
			padding: 0;
			background-color: #000;
	background-size: cover;
			display: flex;
			justify-content: center;
			align-items: center;
			height: 100vh;
			font-family: 'Bad Script',cursive;
			overflow-y: hidden;
		}
		
		h1{
			margin: 0;
			padding: 0;
			color: #111;
			font-size: 50px;
		}

		h1 span {
			font-size: 70px;
			display: table-cell;
			margin: 0;
			padding: 0;
			
			animation:  animate 2s linear infinite;
		}
		h1 span:nth-child(1)
		{
			animation-delay:0s;
		}
		h1 span:nth-child(2)
		{
			animation-delay:0.25s;
		}
		h1 span:nth-child(3)
		{
			animation-delay:0.5s;
		}
		h1 span:nth-child(4)
		{
			animation-delay:0.75s;
		}
		h1 span:nth-child(5)
		{
			animation-delay:1s;
		}
		h1 span:nth-child(6)
		{
			animation-delay:1.25s;
		}
		h1 span:nth-child(7)
		{
			animation-delay:1.5s;
		}
		h1 span:nth-child(8)
		{
			animation-delay:1.75s;
		}
		h1 span:nth-child(9)
		{
			animation-delay:2s;
		}
		h1 span:nth-child(10)
		{
			animation-delay:2.5s;
		}
		h1 span:nth-child(11)
		{
			animation-delay:2.75s;
		}
		h1 span:nth-child(12)
		{
			animation-delay:3s;
		}

		h1 span:nth-child(13)
		{
			animation-delay:3.25s;
		}
		h1 span:nth-child(14)
		{
			animation-delay:3.5s;
		}

		


		@keyframes animate {
			0%,100%

			{
				color: #fff;
				filter: blur(2px);
				text-shadow: 0 0 10px #00b3ff,
							0 0 20px #00b3ff,
							0 0 40px #00b3ff,
							0 0 80px #00b3ff,
						    0 0 120px #00b3ff,
						    0 0 200px #00b3ff,
			     		    0 0 300px #00b3ff,
					        0 0 400px #00b3ff;


			}
			5%,85%

			{
				color: #111;
				filter: blur(0px);
				text-shadow: 0 0 10px none;
			}
		}

		.van {
			font-size: 80px;
		}
		
		
		div {
			margin-top: -10%;
			width: 30%;
			float: left;
		}

		h3 {
			margin-top: -3%;
			background-color: black;
			color: white;
		}
		body {

			background-color: black;
		}
	</style>
</head>
<body>
	<h3><center><video src="manasa.mp4" width="1500" height="500" controls=""> Doest support <code>vedio</code>
	</video></center></h3> 

	<!--<h3><center>
		<video controls="" width="800" height="500" loop="" muted="" autoplay="">
			<source src="manasa.mp4" type="vedio/mp4">
		</video>
	</center></h3>
-->
	<div>

	<basefont><canvas id="canvas"></canvas></basefont>
</div>
	<div>
	<h1>
		
		<span>H</span>
		<span>A</span>
		<span>P</span>
		<span>P</span>
		<span>Y </span>
		<span> <pre class="van"> B</pre></span>
		<span  class="va">I</span>
		<span  class="va">R</span>
		<span  class="va">T</span>
		<span  class="va">H</span>
		<span  class="va">D</span>
		<span  class="va">A</span>
		<span  class="va">Y</span>
	
	</h1>
</div>

	
	
</body>
</html>
