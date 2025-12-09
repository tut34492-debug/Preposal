# Preproposal

## What idea(s) do you have for your final project?

TODO

## If you plan to collaborate with one or two classmates, what are their names?

TODO

## Do you have any questions of your own?

TODO
# Preposal
Idea for initial project fall 2025
# Proposal

## What will (likely) be the title of your project?

the title of my project will be somethng along lines of a simeple game. 

## In just a sentence or two, summarize your project. (E.g., "A website that lets you buy and sell stocks.")

I am planning on making a game, that is going to be really simple in 2D. 

## In a paragraph or more, detail your project. What will your software do? What features will it have? How will it be executed?

I wil be using Godot for my project. I am not completely sure about the rest, but i am planning on doing more research over the weekend. 

## If planning to combine 1051's final project with another course's final project, with which other course? And which aspect(s) of your proposed project would relate to 1051, and which aspect(s) would relate to the other course?

TODO, if applicable

## If planning to collaborate with 1 or 2 classmates for the final project, list their names, email addresses, and the names of their assigned TAs below.

TODO, if applicable

## In the world of software, most everything takes longer to implement than you expect. And so it's not uncommon to accomplish less in a fixed amount of time than you hope.

### In a sentence (or list of features), define a GOOD outcome for your final project. I.e., what WILL you accomplish no matter what?

a good out come of my project is still work in progress, but a good outcome would be Dr.Rosen being able to see the idea that I had behind the project.

### In a sentence (or list of features), define a BETTER outcome for your final project. I.e., what do you THINK you can accomplish before the final project's deadline?

work in progress

### In a sentence (or list of features), define a BEST outcome for your final project. I.e., what do you HOPE to accomplish before the final project's deadline?

still deciding what the project will look like

## In a paragraph or more, outline your next steps. What new skills will you need to acquire? What topics will you need to research? If working with one of two classmates, who will do what?

TODO

# Status Report

#### Your name

Dhruv Satasiya

#### Your section leader's name

N/A

#### Project title

The Gold Hunt

***

Short answers for the below questions suffice. If you want to alter your plan for your project (and obtain approval for the same), be sure to email your section leader directly!

#### What have you done for your project so far?

I have come up with a basic idea to what I am going to do. I made the desigh in the Godot.

#### What have you not done for your project yet?

I just have to fix  the way my character animates when running, and jumping. 

#### What problems, if any, have you encountered?

None



**my code**

extends CharacterBody2D


const SPEED = 400.0
const JUMP_VELOCITY = -900.0
@onready var sprite_2d: AnimatedSprite2D = $Sprite2D

# Get the gravity from the project setings to be synced with RigidBody nodes.
var gravity = ProjectSettings.get_setting("physics/2d/default_gravity")


func _physics_process(delta):
	if (velocity.x > 1 || velocity.x < -1):
		sprite_2d.animation = "running"
	else:
		sprite_2d.animation = "default"
	# Add the gravity.
	if not is_on_floor():
		velocity.y += gravity * delta
		sprite_2d.animation = "jumping"

	# Handle jump.
	if Input.is_action_just_pressed("ui_accept") and is_on_floor():
		velocity.y = JUMP_VELOCITY

	# Get the input direction and handle the movement/deceleration.
	# As good practice, you should replace UI actions with custom gameplay actions.
	var direction = Input.get_axis("ui_left", "ui_right")
	if direction:
		velocity.x = direction * SPEED
	else:
		velocity.x = move_toward(velocity.x, 0, SPEED)

	move_and_slide()
	
	var isLeft = velocity.x < 0
	sprite_2d.flip_h = isLeft
	
	
