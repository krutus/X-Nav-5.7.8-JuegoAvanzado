// Original game from:
// http://www.lostdecadegames.com/how-to-make-a-simple-html5-canvas-game/
// Slight modifications by Gregorio Robles <grex@gsyc.urjc.es>
// to meet the criteria of a canvas class for DAT @ Univ. Rey Juan Carlos

// Create the canvas
var canvas = document.createElement("canvas");
var ctx = canvas.getContext("2d");
canvas.width = 512;
canvas.height = 480;
document.body.appendChild(canvas);

// Background image
var bgReady = false;
var bgImage = new Image();
bgImage.onload = function () {
	bgReady = true;
};
bgImage.src = "images/background.png";

// Hero image
var heroReady = false;
var heroImage = new Image();
heroImage.onload = function () {
	heroReady = true;
};
heroImage.src = "images/hero.png";

// princess image
var princessReady = false;
var princessImage = new Image();
princessImage.onload = function () {
	princessReady = true;
};
princessImage.src = "images/princess.png";

// stone image
var stoneReady = false;
var stoneImage = new Image();
stoneImage.onload = function () {
	stoneReady = true;
};
stoneImage.src = "images/stone.png";

// monster image
var monsterReady = false;
var monsterImage = new Image();
monsterImage.onload=function() {
	monsterReady=true;
};
monsterImage.src = "images/monster.png";

// Game objects
var hero = {
	speed: 256 // movement in pixels per second
};

var princess = {};
var stone = new Array();
stone[0] = {};
stone[1] = {};
var monster = new Array();
monster[0] = {};
monster[1] = {};
var monsterspeed = 10;
var princessesCaught = localStorage.getItem("princessesCaught");
var nivel = localStorage.getItem("nivel");
if (princessesCaught == undefined){
    princessesCaught = 0;
    localStorage.setItem("princessesCaught", princessesCaught);
}
if (nivel == undefined){
    nivel = 1;
    localStorage.setItem("nivel", nivel);
}

            

// Handle keyboard controls
var keysDown = {};

addEventListener("keydown", function (e) {
	keysDown[e.keyCode] = true;
}, false);

addEventListener("keyup", function (e) {
	delete keysDown[e.keyCode];
}, false);

// Reset the game when the player catches a princess
var reset = function () {
	hero.x = canvas.width / 2;
	hero.y = canvas.height / 2;
    	
    if (princessesCaught >= 10) {
			nivel = 2;
			if (princessesCaught >= 20){
			    nivel = 3;
			}
	}	
	
    // Monster's speed
    
    monsterspeed = 5*(princessesCaught);
   
    
    
	//princessesCaught = localStorage.getItem("princessesCaught");
		// Throw the princess somewhere on the screen randomly
	princess.x = Math.random() * (440 - 36) + 36;
	
	princess.y = Math.random() * (420 - 36) + 36;



    // Throw stones somewhere on the screen randomly without collision
    for (i = 0; i < stone.length; i++) {
        do {
		    stone[i].x = 32 + (Math.random() * (canvas.width - 96));
		    stone[i].y = 32 + (Math.random() * (canvas.height - 96));
	    } while (((stone[i].x>hero.x-32 && stone[i].x<hero.x+32) && (stone[i].y<hero.y+32 && stone[i].y>hero.y-32)) ||
        ((stone[i].x>princess.x-32 && stone[i].x<princess.x+32) && (stone[i].y<princess.y+32 && stone[i].y>princess.y-32)))
    };
    
    // Throw the monsters somewhere on the screen randomly without collision
    for (j = 0; j < monster.length; j++){
        do {
		    monster[j].x = 32 + (Math.random() * (canvas.width - 96));
		    monster[j].y = 32 + (Math.random() * (canvas.height - 96));
	    } while (((monster[j].x>hero.x-128 && monster[j].x<hero.x+128) && (monster[j].y<hero.y+128 && monster[j].y>hero.y-128)) ||
        ((monster[j].x>princess.x-32 && monster[j].x<princess.x+32) && (monster[j].y<princess.y+32 && monster[j].y>princess.y-32)))
    };

};


// Update game objects
var update = function (modifier) {
	if (38 in keysDown) { // Player holding up
		if (hero.y >= 36){
			if (!(Math.abs(hero.x - stone[0].x) <= 30 && hero.y - stone[0].y <= 30 && hero.y > stone[0].y) &!
			    (Math.abs(hero.x - stone[1].x) <= 30 && hero.y - stone[1].y <= 30 && hero.y > stone[1].y))    
			{
			hero.y -= hero.speed * modifier;
			}
		}
	}
	if (40 in keysDown) { // Player holding down
		if (hero.y <= 420) {
			if (!(Math.abs(hero.x - stone[0].x) <= 30 && stone[0].y - hero.y <= 30 && hero.y < stone[0].y) &!
			    (Math.abs(hero.x - stone[1].x) <= 30 && stone[1].y - hero.y <= 30 && hero.y < stone[1].y))
			{
			hero.y += hero.speed * modifier;
			}
		}
	}
	if (37 in keysDown) { // Player holding left
		if (hero.x >= 36) {
		    if (!(Math.abs(hero.x - stone[0].x) <= 30 && Math.abs(stone[0].y - hero.y) <= 30 && hero.x > stone[0].x) &!
		        (Math.abs(hero.x - stone[1].x) <= 30 && Math.abs(stone[1].y - hero.y) <= 30 && hero.x > stone[1].x))
			{
		    hero.x -= hero.speed * modifier;
		    }
		}
	}
	if (39 in keysDown) { // Player holding right
		if (hero.x <= 440) {
		    if (!(Math.abs(hero.x - stone[0].x) <= 30 && Math.abs(stone[0].y - hero.y) <= 30 && hero.x < stone[0].x) &!
		        (Math.abs(hero.x - stone[1].x) <= 30 && Math.abs(stone[1].y - hero.y) <= 30 && hero.x < stone[1].x))
			{
		    hero.x += hero.speed * modifier;
		    }
		}
	}
	
	
	
	
	// Monster movement
     for (i = 0; i < monster.length; i++) {
        if (monster[i].x<hero.x &&
            (monster[i].y<=stone[0].y-32 || monster[i].y>=stone[0].y+32 || monster[i].x<=stone[0].x-32 || monster[i].x>=stone[0].x) && 
            (monster[i].y<=stone[1].y-32 || monster[i].y>=stone[1].y+32 || monster[i].x<=stone[1].x-32 || monster[i].x>=stone[1].x)) {
            monster[i].x += monsterspeed * modifier;
        } else if (monster[i].x>hero.x &&
            (monster[i].y<=stone[0].y-32 || monster[i].y>=stone[0].y+32 || monster[i].x<=stone[0].x || monster[i].x>=stone[0].x+32) &&
            (monster[i].y<=stone[1].y-32 || monster[i].y>=stone[1].y+32 || monster[i].x<=stone[1].x || monster[i].x>=stone[1].x+32)) {
            monster[i].x -= monsterspeed * modifier;
        }
        if (monster[i].y<hero.y &&
            (monster[i].y<=stone[0].y-32 || monster[i].y>=stone[0].y || monster[i].x<=stone[0].x-32 || monster[i].x>=stone[0].x+32) &&
            (monster[i].y<=stone[1].y-32 || monster[i].y>=stone[1].y || monster[i].x<=stone[1].x-32 || monster[i].x>=stone[1].x+32)) {
            monster[i].y += monsterspeed * modifier;
        } else if (monster[i].y>hero.y &&
            (monster[i].y<=stone[0].y || monster[i].y>=stone[0].y+32 || monster[i].x<=stone[0].x-32 || monster[i].x>=stone[0].x+32) &&
            (monster[i].y<=stone[1].y || monster[i].y>=stone[1].y+32 || monster[i].x<=stone[1].x-32 || monster[i].x>=stone[1].x+32)){
            monster[i].y -= monsterspeed * modifier;
        }
     }

	// Are they touching?
	if (
		hero.x <= (princess.x + 16)
		&& princess.x <= (hero.x + 16)
		&& hero.y <= (princess.y + 16)
		&& princess.y <= (hero.y + 32)
	) {
	   	++princessesCaught;
	   	localStorage.setItem("princessesCaught", princessesCaught);
		reset();
		
	}
	
	
		
	
	for (i = 0; i < monster.length; i++){
	    if (
            hero.x <= (monster[i].x + 16)
		    && monster[i].x <= (hero.x + 16)
		    && hero.y <= (monster[i].y + 16)
		    && monster[i].y <= (hero.y + 32)
	    ) {
            princessesCaught = 0;
            nivel = 1;
		    reset();
	    }
	};
};

// Draw everything
var render = function () {
	if (bgReady) {
		ctx.drawImage(bgImage, 0, 0);
	}

	if (heroReady) {
		ctx.drawImage(heroImage, hero.x, hero.y);
	}

	if (princessReady) {
		ctx.drawImage(princessImage, princess.x, princess.y);
	}

	if (stoneReady) {
	    for (i = 0; i < stone.length; i++){
		ctx.drawImage(stoneImage, stone[i].x, stone[i].y);
		}
	}
	
	if (monsterReady) {
	    for (j = 0; j < monster.length; j++){
		ctx.drawImage(monsterImage, monster[j].x, monster[j].y);
		}
	}
	
	

	// Score
	ctx.fillStyle = "rgb(250, 250, 250)";
	ctx.font = "12px Helvetica";
	ctx.textAlign = "left";
	ctx.textBaseline = "top";
	ctx.fillText("Princesses caught: " + princessesCaught, 32, 32);
	
	// Level
	ctx.fillStyle = "rgb(250, 250, 250)";
	ctx.font = "12px Helvetica";
	ctx.textAlign = "center";
	ctx.textBaseline = "top";
	ctx.fillText("Level: " + nivel, 64, 64);
};

// The main game loop
var main = function () {
	var now = Date.now();
	var delta = now - then;

	update(delta / 1000);
	render();

	then = now;
};

// Let's play this game!
reset();
var then = Date.now();
//The setInterval() method will wait a specified number of milliseconds, and then execute a specified function, and it will continue to execute the function, once at every given time-interval.
//Syntax: setInterval("javascript function",milliseconds);
setInterval(main, 1); // Execute as fast as possible
