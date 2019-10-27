//Special Thanks and credit to Conor (clasmate) and JieYing (coach) for helping me C:
//Credit for CarlinoGonzalez's rain simulator
//https://www.youtube.com/watch?v=eFaVK3_mWkM


//If want finish project.Intersecting Object
//https://www.youtube.com/watch?v=uAfw-ko3kB8  


var drop = [];
var ball = [];
let x = 0;
let y = 450;
let img;
var move = 250;

//edit game
var wide = 1000;
var boatsp = 40;
var Csize = 60;
var rise = .2;
var ballsp1 = 5;
var ballsp2 = 10;
var amountball = 5;
var controlball = 5; //how much go back up

function preload() {
  img = loadImage("img/boat.png");
  cannon = loadSound("cannon.wav");
  rain = loadSound("rain.mp3");
  win = loadSound("win.mp3");
  lose = loadSound("lose.wav");
  win_hero = loadSound("win_hero.wav")

}

function setup() {
  createCanvas(wide, 500);
  rain.loop();
  rain.setVolume(0.5)

  for (var i = 0; i < 150; i++) {
    drop[i] = new Drop();
  }
  for (var i = 0; i < amountball; i++) {
    ball[i] = new Ball(); //varible ball [i]
    size = random(30, 40);

    //img [k] = new Boat();           WIP intersection**

  }

}

function draw() {
  background(100);


  for (var i = 0; i < 150; i++) { //amount rain
    drop[i].show();
    drop[i].update();
  }

  for (var j = 0; j < amountball; j++) {
    ball[j].show();
    ball[j].update();
  }


  for (var i = 0; i < 1; i = i + 1) {

    if (y > 60) {
      fill(255, 255, 255);
      rect(x, y, wide, 900);
      y = y - rise; //rising water


      image(img, move, y - 60, 80, 60); //boat image
    } else {
      y = 60;

      fill(255, 255, 255);
      rect(x, y, wide, 900);
      image(img, move, y - 60, 80, 60); //boat image
      noLoop();
      win_hero.play();


    }

  }
  if (move < 0) { //boundary movement ship
    move = 0;
  }
  if (move > width - 80) {
    move = width - 80;
  }
}

function Drop() { //rain
  this.x = random(0, width);
  this.y = random(0, -height);

  this.show = function() {
    noStroke();
    fill(255);
    ellipse(this.x, this.y, 2, 10);
  }

  this.update = function() {
    this.speed = random(5, 20);
    this.y = this.y + this.speed;

    if (this.y > height) {
      this.y = random(0, -height);
    }
  }
}

function Ball() { //cannon class explaination: a group?
  this.x = random(0, width);
  this.y = 0;
  //this.r = Csize;

  this.show = function() {
    noStroke();
    fill(179, 209, 10);
    ellipse(this.x, this.y, Csize, Csize);
  }

  this.update = function() {
    this.speed = random(ballsp1, ballsp2);
    this.y = this.y + this.speed;

    if (this.y > height) {
      this.y = 0;


    }
    // function Boat() {           WIP intersection**
    //   this.x = 
    //   this.y =

  }
}

function keyPressed() { //controls 
  if (keyCode === LEFT_ARROW) {
    move = move - boatsp;
  } else if (keyCode === RIGHT_ARROW) {
    move = move + boatsp;
  }

  if (key === "c") {
    for (var i = 0; i < controlball; i++) {
      ball[i] = new Ball();
      size = random(30, 40);
      cannon.play();
      cannon.setVolume(0.1)

    }

  }

}
