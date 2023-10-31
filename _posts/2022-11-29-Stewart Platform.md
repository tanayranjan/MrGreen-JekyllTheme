---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: id_stewart_p
title: "Stewart Platform"

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Tanay Ranjan
# multiple category is not supported
category: Projects
# multiple tag entries are possible 
tags: [arduino, onshape, cad, servo]
# thumbnail image for post
img: ":StewartPlatform/2.png"
# disable comments on this page
#comments_disable: true

# publish date
date: 2022-11-29 10:04:30 +0900

# seo
# if not specified, date will be used.
#meta_modify_date: 2022-01-01 10:04:30 +0900
# check the meta_common_description in _data/owner/[language].yml
#meta_description: ""

# optional
# please use the "image_viewer_on" below to enable image viewer for individual pages or posts (_posts/ or [language]/_posts folders).
# image viewer can be enabled or disabled for all posts using the "image_viewer_posts: true" setting in _data/conf/main.yml.
#image_viewer_on: true
# please use the "image_lazy_loader_on" below to enable image lazy loader for individual pages or posts (_posts/ or [language]/_posts folders).
# image lazy loader can be enabled or disabled for all posts using the "image_lazy_loader_posts: true" setting in _data/conf/main.yml.
#image_lazy_loader_on: true
# exclude from on site search
#on_site_search_exclude: true
# exclude from search engines
#search_engine_exclude: true
# to disable this page, simply set published: false or delete this file
#published: false
image_sliders:
  - stewart
---

# Aim:

To fabricate Stewart Platform, and control it with Arduino

---

# Components Used:

1. Arduino Uno
2. MG995 Servos x 6
3. Servo Horns x 6
4. Rod End Bearing Spherical Joints - 6mm x 12
5. Metal shafts with threading - 6mm x 6
6. LM2596S DC-DC Buck Converter x 3 
7. Power Source AC-DC 12V-2A supply
8. Screws and nuts- M3 x 6
9. Jumper Wires

---

# 3D Printed Parts:

1. Upper Base x 1

	![57a2bddcdc0b02bc1e7dde2dfc4587f4.png](:StewartPlatform/57a2bddcdc0b02bc1e7dde2dfc4587f4.png)
	
  Used as upper part of the system, which we are supposed to move. 
	It has extrusion for the "Rod End Bearing Spherical Joints"
	
2. Connector x 6

	![ac81e1a248155f420b5fb6678cda511b.png](:StewartPlatform/ac81e1a248155f420b5fb6678cda511b.png)
	
  Used for connecting hole of "Rod End Bearing Spherical Joints" (6 mm), to the hole of Servo horns (3 mm)

---
	
# Fabricated Model

{% include slider.html selector="stewart" %}
	
---

# Circuit Diagram

![7cbfa197d76653dd46fc7774bac3845f.png](:StewartPlatform/7cbfa197d76653dd46fc7774bac3845f.png)

---

# Implementation

<iframe width="560" height="315" src="https://www.youtube.com/embed/jKpzDBAMBiE?si=ZQ2Y4JkuWsYi0A1h" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

---

## Vertical Motion

The upper base moving vertical up and down

<iframe src="https://drive.google.com/file/d/1BKhRoIAakjQp8SDqGbaVQaWgeVYjym_E/preview" width="640" height="480" allow="autoplay"></iframe>

<!-- <details>
  <summary><b>Click</b></summary>

  <pre>
  <span style="color:grey">
  ```js
  function logSomething(something) {
    console.log('Something', something);
  }
  ```
  </span>
  </pre>

</details> -->





<!-- Code:

```Arduino
#include <Servo.h>
Servo Servo1;
Servo Servo2;
Servo Servo3;
Servo Servo4;
Servo Servo5;
Servo Servo6;

// Servo Pin numbers
int servoPin1 = 5;
int servoPin2 = 6;
int servoPin3 = 9;
int servoPin4 = 11;
int servoPin5 = 10;
int servoPin6 = 3;

void setup() {
  // Servo pins setup
  Servo1.attach(servoPin1);
  Servo2.attach(servoPin2);
  Servo3.attach(servoPin3);
  Servo4.attach(servoPin4);
  Servo5.attach(servoPin5);
  Servo6.attach(servoPin6);
}

void loop() {
   //To move the platform vertically up and down
  int i = 0;
  int j = 0;
  while(i <= 90) {
    j =180 - i;
    Servo1.write(i);
    Servo2.write(j);
    Servo3.write(i);
    Servo4.write(j);
    Servo5.write(i);
    Servo6.write(j);

    delay(25);

    i += 1;
  }
//  Servo1.write(45);
//  Servo2.write(135);
//  Servo3.write(45);
//  Servo4.write(135);
//  Servo5.write(45);
//  Servo6.write(135);
  while(i >= 0) {
    j =180 - i;
    Servo1.write(i);
    Servo2.write(j);
    Servo3.write(i);
    Servo4.write(j);
    Servo5.write(i);
    Servo6.write(j);

    delay(25);

    i -= 1;
  }

}
``` -->

## Twisting Motion

Twisting the upper plane with respect to vertical axis

<iframe src="https://drive.google.com/file/d/14v_31YpnsDLOFqjI-beK3KBMPaJUY2Jy/preview" width="640" height="480" allow="autoplay"></iframe>


<!-- Code: -->

<!-- ```Arduino
#include <Servo.h>

Servo Servo1;
Servo Servo2;
Servo Servo3;
Servo Servo4;
Servo Servo5;
Servo Servo6;

int servoPin1 = 5;
int servoPin2 = 6;
int servoPin3 = 9;
int servoPin4 = 11;
int servoPin5 = 10;
int servoPin6 = 3;

void setup() {
  // put your setup code here, to run once:
  Servo1.attach(servoPin1);
  Servo2.attach(servoPin2);
  Servo3.attach(servoPin3);
  Servo4.attach(servoPin4);
  Servo5.attach(servoPin5);
  Servo6.attach(servoPin6);
}

void loop() {
  // put your main code here, to run repeatedly:
  int i = 45;
  int theta = 15;
  while(i <= 45+theta) {
    Servo1.write(i);
    Servo2.write(90+i);
    Servo3.write(i);
    Servo4.write(90+i);
    Servo5.write(i);
    Servo6.write(90+i);

    delay(75);

    i++;
  }

  while(i >= 45-theta) {
    Servo1.write(i);
    Servo2.write(90+i);
    Servo3.write(i);
    Servo4.write(90+i);
    Servo5.write(i);
    Servo6.write(90+i);

    delay(75);

    i--;
  }


  while(i <= 45) {
    Servo1.write(i);
    Servo2.write(90+i);
    Servo3.write(i);
    Servo4.write(90+i);
    Servo5.write(i);
    Servo6.write(90+i);

    delay(75);

    i++;
  }
}
``` -->

## Horizontal Circular Motion

Moving the whole upper plane in it's plane in a circular motion

<iframe src="https://drive.google.com/file/d/1gB_VU66TVtDA0-qJjip9Ou__tl_UeeYr/preview" width="640" height="480" allow="autoplay"></iframe>

<!-- Code:
```Arduino
#include <Servo.h>

Servo Servo1;
Servo Servo2;
Servo Servo3;
Servo Servo4;
Servo Servo5;
Servo Servo6;

int servoPin1 = 5;
int servoPin2 = 6;
int servoPin3 = 9;
int servoPin4 = 11;
int servoPin5 = 10;
int servoPin6 = 3;

void setup() {
  // put your setup code here, to run once:
  Servo1.attach(servoPin1);
  Servo2.attach(servoPin2);
  Servo3.attach(servoPin3);
  Servo4.attach(servoPin4);
  Servo5.attach(servoPin5);
  Servo6.attach(servoPin6);
}

void loop() {
  int i = 45;
  while(i <= 90) {
    Servo1.write(90-i);
    Servo2.write(90+i);
    Servo3.write(45);
    Servo4.write(135);
    Servo5.write(i);
    Servo6.write(180-i);

    delay(75);
    i++;
  }

  int counter = 0;
  while(counter < 5) {
    i = 0;
    while(i <= 45) {
      Servo1.write(i);
      Servo2.write(180-i);
      Servo3.write(45+i);
      Servo4.write(135-i);
      Servo5.write(90-2*i);
      Servo6.write(90+2*i);

      delay(75);
      i++;
    }

    i = 0;
    while(i <= 45) {
      Servo5.write(i);
      Servo6.write(180-i);
      Servo1.write(45+i);
      Servo2.write(135-i);
      Servo3.write(90-2*i);
      Servo4.write(90+2*i);

      delay(75);
      i++;
    }

    i = 0;
    while(i <= 45) {
      Servo3.write(i);
      Servo4.write(180-i);
      Servo5.write(45+i);
      Servo6.write(135-i);
      Servo1.write(90-2*i);
      Servo2.write(90+2*i);

      delay(75);
      i++;
    }

    counter++;
  }

  i = 0;
  while(i <= 45) {
    Servo1.write(i);
    Servo2.write(180-i);
    Servo3.write(45);
    Servo4.write(135);
    Servo5.write(90-i);
    Servo6.write(90+i);

    delay(75);
    i++;
  }
}
``` -->


## For Code of this Project, [Click here](https://github.com/webisgood/Design_and_Testing_of_Stewart_Platform)

