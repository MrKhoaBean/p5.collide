# p5.collide
#### A 2d collision detection module for nodejs
p5.collide provides tools for calculating collision detection for 2D geometry.

p5.collide contains some versions of, and references to, the functions in [Jeffrey Thompson's Collision Detection Book](http://www.jeffreythompson.org/collision-detection/). His code is [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), so, this is too! I highly, highly, reccomend [reading his book](http://www.jeffreythompson.org/collision-detection/) to better understand all of the details involved in collision detection. Implementing this library into your code will be much easier and more efficent after reading it!

It's an incredible resource for this kind of work! – [http://www.jeffreythompson.org/collision-detection/](http://www.jeffreythompson.org/collision-detection/)

All p5.collide functions return `true` if the specified geometry is colliding and `false` if they are not.


## Install
```javascript
npm install p5.collide
```

## Table of Contents

##### 2D Collision Detection
  + [collidePointPoint()](#collidepointpoint)
  + [collidePointCircle()](#collidepointcircle)
  + [collidePointEllipse()](#collidepointellipse)
  + [collidePointRect()](#collidepointrect)
  + [collidePointLine()](#collidepointline)
  + [collideRectRect()](#colliderectrect)
  + [collideCircleCircle()](#collidecirclecircle)
  + [collideRectCircle()](#colliderectcircle)
  + [collideLineLine()](#collidelineline)
  + [collideLineCircle()](#collidelinecircle)
  + [collideLineRect()](#collidelinerect)
  + [collidePointPoly()](#collidepointpoly)
  + [collideCirclePoly()](#collidecirclepoly)
  + [collideRectPoly()](#colliderectpoly)
  + [collideLinePoly()](#collidelinepoly)
  + [collidePolyPoly()](#collidepolypoly)
  + [collidePointTriangle()](#collidepointtriangle)

## p5.collide examples & documentation

#### collidePointPoint()
###### collidePointPoint(x, y, x2, y2, [buffer])
Point to point collision with an optional buffer zone.
```javascript
//basic 2D example
var hit = false;
function draw() {
	background(255);
	ellipse(100,100,1,1); //change to 10,10px size for buffer example
	ellipse(mouseX,mouseY,1,1); //change to 10,10px size for buffer example

	//no buffer zone, most standard example
	hit = collidePointPoint(100,100,mouseX,mouseY)

	//buffer of 10 px
	//hit = collidePointPoint(100,100,mouseX,mouseY,10)

	print("colliding? " + hit);
}
```

#### collidePointCircle()
###### collidePointCircle(pointX, pointY, circleX, circleY, diameter)
point to circle collision in 2D. Assumes ellipseMode(CENTER);
```javascript
var hit = false;
function draw() {
	background(255);
	ellipse(200,200,100,100);
	point(mouseX,mouseY);

	hit = collidePointCircle(mouseX,mouseY,200,200,100)

	print("colliding? " + hit);

}
```

#### collidePointEllipse()
###### collidePointEllipse(pointX, pointY, ellipseX, ellipseY, ellipseWidth, ellipseHeight )
point ellipse collision. It takes the point, the centre of the ellipse, the major and the minor axes (diameters).

![point ellipse collision](https://user-images.githubusercontent.com/13430702/47784680-98543d80-dd06-11e8-8814-47a37186263a.png)

```javascript
let hit = false;
function draw(){
	background(255);
	ellipse(200,200,50,150);
	point(mouseX,mouseY);

	hit = collidePointEllipse(mouseX,mouseY,200,200,50,150)

	print("colliding? " + hit);
}
```

#### collidePointRect()
###### collidePointRect(pointX, pointY, x, y, width, height)
point to rect collision in 2D. Assumes rectMode(CORNER);
```javascript
var hit = false;
function draw() {
  background(255);
	rect(200,200,100,150);

	hit = collidePointRect(mouseX,mouseY,200,200,100,150);

	print("colliding? " + hit);

}
```
#### collidePointLine()
###### collidePointLine(pointX, pointY, x, y, x2, y2, [buffer])
point to line collision in 2D, includes and optional buffer which expands the hit zone on the line (default buffer is 0.1).
```javascript
var hit = false;
function draw(){
  background(255);
	line(200,300,100,150);
	point(mouseX,mouseY);

  //collide point line using the optional buffer with a 0.5 value
	hit = collidePointLine(mouseX,mouseY,200,300,100,150, 0.5);

	print("colliding? " + hit);
}
```
#### collideCircleCircle()
###### collideCircleCircle(circleX, circleY,circleDiameter, circleX2, circleY2, circleDiameter2)
circle to circle collision in 2D. Assumes ellipseMode(CENTER);

```javascript
var hit = false;
function draw() {
	background(255);
	ellipse(200,200,100,100);
	ellipse(mouseX,mouseY,150,150);

	hit = collideCircleCircle(mouseX,mouseY,150,200,200,100)

	print("colliding? " + hit);

}
```

#### collideRectRect()
###### collideRectRect(x, y, width, height, x2, y2, width2, height2 )
rect rect collision in 2D. Assumes rectMode(CORNER);

```javascript
var hit = false;
function draw() {
  background(255);
	rect(200,200,100,150);
	rect(mouseX,mouseY,50,75);

	hit = collideRectRect(200,200,100,150,mouseX,mouseY,50,75);

	print("colliding? " + hit);

}
```

#### collideRectCircle()
###### collideRectCircle(x1, y1, width1, height1, cx, cy, diameter)
rect circle collision in 2D. Assumes rectMode(CORNER) && ellipseMode(CENTER);

```javascript
var hit = false;
function draw() {
  background(255);
	rect(200,200,100,150);
	ellipse(mouseX,mouseY,100,100);

	hit = collideRectCircle(200,200,100,150,mouseX,mouseY,100);

	print("colliding? " + hit);
}
```
#### collideLineLine()
###### collideLineLine(x1, y1, x2, y2, x3, y3, x4, y4, [calcIntersection])
line to line collision in 2D. Takes an optional boolean parameter which calculates the intersection point. If enabled it will return an object containing the x,y position of the collision intersection. If no intersection occurs, it will return an object containing x,y values as false.

```javascript
//basic example
var hit = false;
function draw(){
  background(255);
  line(200,300,100,150);
  line(mouseX,mouseY,350,50);
  hit = collideLineLine(200,300,100,150,mouseX,mouseY,350,50);

  print("colliding? " + hit);
}
```
```javascript
//Return an object containing the x,y position of the intersection using the optional calcIntersection boolean
var hit = false;
function draw(){
  background(255);
  line(200,300,100,150);
  line(mouseX,mouseY,350,50);

  hit = collideLineLine(200,300,100,150,mouseX,mouseY,350,50,true);

  print("X-intersection:" + hit.x);
  print("Y-intersection:" + hit.y);
}
```

#### collideLineCircle()
###### collideLineCircle(x1,  y1,  x2,  y2,  cx,  cy,  diameter)
point to circle collision in 2D.
```javascript
var hit = false;
function draw(){
  background(255);
	line(200,300,100,150);
	ellipse(mouseX,mouseY,50,50);
	hit = collideLineCircle(200,300,100,150,mouseX,mouseY,50);

	print("colliding? " + hit);

}
```
#### collideLineRect()
###### collideLineRect(x1, y1, x2, y2, rx, ry, rw, rh, [calcIntersection])
Line to Rectangle collision in 2d. Takes and optional boolean parameter which calculates the intersection points. If enables it will return an object containing objects of the top,left,bottom,right X,Y intersection positions. If no intersection occurs, it will return an object containing x,y values as false.

```javascript
//basic example
var hit = false;
function draw() {
	background(255);
	rect(200,300,100,150);
	line(mouseX,mouseY,350,50);

	hit = collideLineRect(mouseX,mouseY,350,50,200,300,100,150);

	print("colliding? " + hit);
}
```

```javascript
//Return an object containing the x,y position of the bottom intersection of the rect using the optional calcIntersection boolean.
var hit = false;
function draw() {
	background(255);
	rect(200,300,100,150);
	line(mouseX,mouseY,350,50);

	hit = collideLineRect(mouseX,mouseY,350,50,200,300,100,150,true);

  //retruned object contains top,right,bottom,left objects which each contain x,y values.
  print("bottomX: " + hit.bottom.x);
  print("bottomY: " + hit.bottom.y);
  print("topX: " + hit.top.x);
  print("topY: " + hit.top.y);
  print("leftX: " + hit.left.x);
  print("leftY: " + hit.left.y);
  print("rightX: " + hit.right.x);
  print("rightY: " + hit.right.y);
}
```
#### collidePointPoly()
###### collidePointPoly(pointX,pointY,vectorArray)
Point to Poly Collision in 2D. Takes a point x,y and an array of [p5.Vector](http://p5js.org/reference/#/p5/createVector) points which contain the x,y positions of the polygon. This function works with x-sided polygons, and "collapsed" polygons where a single polygon shape overlaps itself.

```javascript
var hit = false;
var poly = []; //store the vertices for our polygon
function setup() {
	createCanvas(500,500);
	poly[0] = createVector(123,231);     // set X/Y positions
	poly[1] = createVector(10,111);
	poly[2] = createVector(20,23);
	poly[3] = createVector(390,33);
}

function draw() {
	background(255);

  //draw the polygon from the created Vectors above.
	beginShape();
	for(i=0; i < poly.length; i++){
		vertex(poly[i].x,poly[i].y);
	}
	endShape(CLOSE);

	ellipse(mouseX,mouseY,10,10); //put a small ellipse on our point.

	hit = collidePointPoly(mouseX,mouseY,poly); //3rd parameter is an array of vertices.

	print("colliding? " + hit);
}
```
#### collideCirclePoly()
###### collideCirclePoly(x,y,diameter,vectorArray, [interiorCollision])
Circle to Poly Collision in 2D. Takes a circle x,y,diameter and an array of [p5.Vector](http://p5js.org/reference/#/p5/createVector) points which contain the x,y positions of the polygon. This function works with x-sided polygons, and "collapsed" polygons where a single polygon shape overlaps itself. Takes an optional 5th 'true' boolean parameter which enables the collision detection if the circle is wholly inside the polygon. The interior detection is off by default to save evaluating all of the edges of the polygon a second time.

```javascript
var hit = false;
var poly = [];
function setup() {
	createCanvas(windowWidth,windowHeight);
	poly[0] = createVector(123,231);     // set X/Y position
	poly[1] = createVector(10,111);
	poly[2] = createVector(20,23);
	poly[3] = createVector(390,33);
}

function draw() {
	background(255);

  //draw the polygon from the created Vectors above.
	beginShape();
	for(i=0; i < poly.length; i++){
		vertex(poly[i].x,poly[i].y);
	}
	endShape(CLOSE);

	ellipse(mouseX,mouseY,45,45);

	hit = collideCirclePoly(mouseX,mouseY,45,poly);
	//enable the hit detection if the circle is wholly inside the polygon
	// hit = collideCirclePoly(mouseX,mouseY,45,poly,true);

	print("colliding? " + hit);
}
```

#### collideRectPoly()
###### collideRectPoly(x,y,width,height,vectorArray, [interiorCollision])
Rect to Poly Collision in 2D. Takes a rect x,y,width,height and an array of [p5.Vector](http://p5js.org/reference/#/p5/createVector) points which contain the x,y positions of the polygon. This function works with x-sided polygons, and "collapsed" polygons where a single polygon shape overlaps itself. Takes an optional 6th 'true' boolean parameter which enables the collision detection if the rect is wholly inside the polygon. The interior detection is off by default to save evaluating all of the edges of the polygon a second time.

```javascript
var hit = false;
var poly = [];
function setup() {
	createCanvas(windowWidth,windowHeight);
	poly[0] = createVector(323,431);     // set X/Y position
	poly[1] = createVector(210,311);
	poly[2] = createVector(220,223);
	poly[3] = createVector(590,233);
}

function draw() {
	background(255);
	push()
	beginShape();
	//draw the polygon from the created Vectors above.
	for(i=0; i < poly.length; i++){
		vertex(poly[i].x,poly[i].y);
	}
	endShape(CLOSE);

	rect(mouseX,mouseY,45,100);

	hit = collideRectPoly(mouseX,mouseY,45,100,poly);
	//enable the hit detection if the circle is wholly inside the polygon
	// hit = collideRectPoly(mouseX,mouseY,45,100,poly,true);

	print("colliding? " + hit);
}
```
#### collideLinePoly()
###### collideLinePoly(x1, y1, x2, y2, vertices)
Line to Poly Collision in 2D. Takes a line x,y,x2,y2 and an array of [p5.Vector](http://p5js.org/reference/#/p5/createVector) points which contain the x,y positions of the polygon. This function works with x-sided polygons, and "collapsed" polygons where a single polygon shape overlaps itself.

```javascript
var hit = false;
var poly = new Array(16);
function setup() {
	createCanvas(windowWidth,windowHeight);

	//generate a 16 sided polygon
  var angle = TWO_PI / poly.length;
  for (var i=0; i<poly.length; i++) {
    var a = angle * i;
    var x = 300 + cos(a) * 100;
    var y = 200 + sin(a) * 100;
    poly[i] = createVector(x,y);
  }
}
function draw() {
	background(255);
	beginShape();
	//draw the polygon from the created Vectors above.
	for(i=0; i < poly.length; i++){
		vertex(poly[i].x,poly[i].y);
	}
	endShape(CLOSE);

	line(10,10,mouseX,mouseY);

	hit = collideLinePoly(mouseX,mouseY,45,100,poly);

	print("colliding? " + hit);
}
```
#### collidePolyPoly()
###### collidePolyPoly(polygon1, polygon2, [interiorCollision])
Polygon to Polygon Collision in 2D. Takes a 2 arrays of [p5.Vector](http://p5js.org/reference/#/p5/createVector) points which contain the x,y positions of the polygons. This function works with x-sided polygons, and "collapsed" polygons where a single polygon shape overlaps itself. Takes an optional 3rd 'true' boolean parameter which enables the collision detection if the polygon is wholly inside the other polygon. The interior detection is off by default to save evaluating all of the edges of the polygon a second time.

```javascript
//example adapted from Jeffrey Thompson
var hit = false;
var poly = new Array(8);
var randomPoly = []
function setup() {
	createCanvas(windowWidth,windowHeight);

	//generate a uniform sided polygon
  var angle = TWO_PI / poly.length;
  for (var i=0; i<poly.length; i++) {
    var a = angle * i;
    var x = 300 + cos(a) * 100;
    var y = 200 + sin(a) * 100;
    poly[i] = createVector(x,y);
  }

  // create a random polygon
  var a = 0;
  var i = 0;
  while (a < 360) {
    var x = cos(radians(a)) * random(30,50);
    var y = sin(radians(a)) * random(30,50);
    randomPoly[i] = createVector(x,y);
    a += random(15, 40);
    i += 1;
  }
}
function draw() {
	background(255);
	 // update random polygon to mouse position
  var mouse = createVector(mouseX, mouseY);
  var diff = mouse.sub(randomPoly[0]);

  for (i=0; i < randomPoly.length; i++) {
    randomPoly[i].add(diff);
  }

	beginShape();
	//draw the polygon from the created Vectors above.
	for(i=0; i < poly.length; i++){
		vertex(poly[i].x,poly[i].y);
	}
	endShape(CLOSE);
	beginShape();
	for(i=0; i < randomPoly.length; i++){
		vertex(randomPoly[i].x,randomPoly[i].y);
	}
	endShape(CLOSE);

	hit = collidePolyPoly(poly,randomPoly,true);
	print("colliding? " + hit);

}
```

#### collidePointTriangle()
###### collidePointTriangle(px, py, x1, y1, x2, y2, x3, y3)
Point to Triangle collision in 2D. You could use [collidePointPoly()](#collidepointpoly) to do this as well, but this is more efficient.
```javascript
var hit = false;
function draw() {
	background(255);
	triangle(300,200,350,300,250,300)
	ellipse(mouseX,mouseY,10,10);

	hit = collidePointTriangle(mouseX,mouseY, 300,200,350,300,250,300)
	print("colliding? " + hit)
}
```
## Source
```javascript
https://github.com/bmoren/p5.collide2D
```
