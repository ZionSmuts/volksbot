# The Volksbot

### Welcome to the *not official* Volksbot Repository :)

<p align="center">
  <img src="images/chassis-side-view" alt="Chassis" width="350"/>
</p>

I am just an engineering student currently doing my internship at a laser scanning company, where I was given this so-called "Volksbot" to fix — and hopefully drive again.

If you are looking for information about the Volksbot, you won’t find much on the internet beyond catalogues and scientific papers that cover the general purpose of the Volksbot and its siblings (I’ve really tried to find more, but without much success). The "official" website (www.volksbot.de) isn’t too useful either, as it is currently for sale. So this repository is my attempt to bring the project back to life!

---

## What is the end goal for this project?

My ultimate goal with this Volksbot is simply to get it moving again. *How* I do that isn’t important for the company — just that it moves. Once it does, we plan to mount one of the company’s custom-built laser scanners on top of the Volksbot (which I may also call “the rover” in the future) and drive around scanning the surroundings. While the rover moves with the scanner mounted, the data will be processed into the company’s dedicated app, letting you view the environment in 3D on a tablet or device of your choice.

**Note:** I unfortunately won’t be covering the laser scanner itself in detail, as my understanding of the deeper, complex topics behind its design is not there yet.

---

## How will the Volksbot move?

The first plan is to control the rover using a Logitech F710 gaming controller (referred to as a “joystick” from now on) through ROS 2 packages. The reason for using ROS 2 is that there is an incredible amount of information online about similar projects. It also gives me the option in the future, to make the rover autonomous. Where if this first step is successful, I definietly plan to do.

<p align="center">
  <img src="images/Logitech.jpg" alt="Logitech Game Controller" width="350"/>
</p>

At the moment, I will be using **Ubuntu 20.04 with ROS 2 Foxy** to simulate and test the Volksbot. You are, of course, welcome to use newer versions of Ubuntu, but I was advised that 20.04 is less buggy. Another important factor is that the embedded compute module I’ll be using — the *NVIDIA Jetson AGX Xavier* — also runs on Ubuntu 20.04, and I’d rather not change that to avoid trouble xD

---

## Why this repo?

This is the journey of figuring things out, documenting as much as possible, and hopefully leaving behind solid documentation for a project that has become almost non-existent online. The goal is that the next person who takes over will have a much easier time.

**Note:** Please also read the `README.md` files in the subfolders (`hardware/`, `power_electronics/`, `mechanical/`, `software/`). They contain details about the current state of the Volksbot and notes on how I overcame problems along the way.
