# Birthday Mini Game Made for Co-Worker

Small project made for a co-worker. Quickly coded and not at all optimized, but the main scripts are below:


## Autoload Singleton Script
```gdscript
# Globals.gd
extends Node

var Achievements = ""
```

## Start Screen Script
```gdscript
# Start.gd
extends Control


func _on_Button_button_down():
	Globals.Achievements = ""
	get_tree().change_scene("res://Main.tscn")
```

## End Script
```gdscript
# End.gd
extends Control

onready var story_text = $VBoxContainer/Story

var achievement_list = []
var story = ""
var displayed_story = ""
var progress = 0


func _ready():
	create_achievement_list(Globals.Achievements)
	build_story()
	story_text.text = story
	story_text.visible_characters = 0


func _process(delta):
	if story_text.visible_characters < story.length():
		story_text.visible_characters += 1


func create_achievement_list(achievements):
	for letter in achievements:
		achievement_list.append(letter)


func build_story():
	story += "Your party begins."
	# PARKADE
	story += "\n"
	story += "\n"
	if achievement_list.has("A"):
		story += "People oddly remark that there were no accidents in the parkade today! Strange that they would bring this up, but great!"
	elif achievement_list.has("B"):
		story += "People mention that there were, unfortunately, a few minor accidents in the parkade today."
	else:
		story += "People are shocked at the amount of accidents in the parkade today! They also comment on the abundance of work orders generated regarding the lights in the parkade. You quietly sit and think, 'Oops.'"
	# SMELL
	story += "\n"
	story += "\n"
	if achievement_list.has("C"):
		story += "As people continue to chat at your party, you take a deep breath in and think, 'Wow, this place smells okay.'"
	elif achievement_list.has("D"):
		story += "As people continue to chat at your party, you take a deep breath in and think, 'Wow, this place smells okay.' You open your eyes and see Luke looking back at you. He looks slightly annoyed that you threw his lunch on the ground."
	else:
		story += "As people continue to chat at your party, you take a deep breath in and think, 'Something smells off... why does this building smell like Indian Fusion?' You open your eyes and see Luke looking back at you. 'Do you smell that odour?' he asks. You nod and get back to the party."
	# MIKE
	story += "\n"
	story += "\n"
	if achievement_list.has("E"):
		story += "You look around and are happy to see how many people showed up to your party. Mike says, 'Cheers!' and you notice the loser fob hanging around his neck."
	else:
		story += "You look around and are happy to see how many people showed up to your party. You notice Mike is not present, but at that moment hear your phone beep. There is a text messages from Mike that says, 'I'm stuck in the stairs without a fob. Please help.'"
	# HEATHER & JAMES
	story += "\n"
	story += "\n"
	if achievement_list.has("F"):
		story += "A guest at the party mentions that all the milk is missing from each floor. At that moment, Heather and James enter the party and place a carton of milk in front of everyone. 'OPEN THEM!' they yell. People nervously look around and open the milk cartons. You open your milk carton. No one fails the test. The milk carton culprit lives on."
	elif achievement_list.has("G"):
		story += "Heather and James suddenly enter the party and say, 'We believe we have caught the milk carton culprit! It is Britt!' People look around awkwardly and seem confused. After a moment of silence things seem to go back to normal."
	else:
		story += "Heather and James suddenly enter the party and say, 'We know you are out there, Milk Carton Culprit! It's only a matter of time before we find you.' People look around awkwardly and seem confused. After a moment of silence things seem to go back to normal."
	# ICT USB STICK
	story += "\n"
	story += "\n"
	if achievement_list.has("I"):
		story += "ICT staff enter your party and bring you an extra cake! They say that you found a very dangerous USB stick and saved the organization from a virus!"
	elif achievement_list.has("J"):
		story += "During the party you put your hand in your pocket and remember that you still have the USB stick you found. You decide you will quickly check its contents. Your computer sparks as you plug it in and the building loses power. The generator activates and you again ponder the ICT training. 'Whoops,' you think to yourself."
	else:
		story += "You have a strange feeling that a dangerous presence lurks in the building. Although not sure, you feel it is digital in nature. 'Strange...' you think to yourself."
	# CLOSE
	story += "\n"
	story += "\n"
	story += "What a strange day."


func _on_Button_button_down():
	get_tree().change_scene("res://Start.tscn")

```

## Main Script
```gdscript
# Main.gd
extends Control

onready var location_text = $VBox/PanelContainer2/HBoxTop/LocationText
onready var scenario = $VBox/Scenario
onready var image = $VBox/CenterContainer/TextureRect
onready var button1 = $VBox/PanelContainer/VBoxChoices/Button1
onready var button2 = $VBox/PanelContainer/VBoxChoices/Button2
onready var button3 = $VBox/PanelContainer/VBoxChoices/Button3
onready var button4 = $VBox/PanelContainer/VBoxChoices/Button4

var button1_dest = 0
var button2_dest = 0
var button3_dest = 0
var button4_dest = 0

var stories = [
		# STORY 0
	{
		"location": "Parkade P2",
		"scenario": "You arrive to work early with hopes of having a quiet morning to get some work done before your party. However, upon arrival you notice that all the parkade lights are off. As you exit your vehicle, you realize the quiet morning you had hoped for is probably not going happen. What do you do?",
		"button1": "Pull out your cell phone, access the DDC system, and manually turn the lights on.",
		"button2": "Call maintenance. They can fix this later.",
		"button3": "Deal with this later - you have more important things to do, like getting to your party.",
		"button4": "Get back in the car, go home. You don't need this today.",
		"button1_dest": 2,
		"button2_dest": 3,
		"button3_dest": 4,
		"button4_dest": 1,
		"image": "res://images/0_dark_parkade.png",
		"achievement": "",
	},
		# STORY 1
	{
		"location": "Highway #1",
		"scenario": "You run back to your car, head to the highway, and are outta here! Well... eventually you will be outta here. After waiting for awhile you realize you are not getting home anytime soon and your party is about to begin. You head back to the party until traffic clears.",
		"button1": "Woohoo party! Boo traffic!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": "end",
		"button2_dest": 0,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/1_traffic.jpg",
		"achievement": "",
	},
		# STORY 2
	{
		"location": "Parkade P2",
		"scenario": "You got the lights back on! Time to head upstairs - do you take the elevator or the stairs?",
		"button1": "Elevator.",
		"button2": "Stairs.",
		"button3": "",
		"button4": "",
		"button1_dest": 5,
		"button2_dest": 6,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/2_parkade.jpg",
		"achievement": "A",
	},
		# STORY 3
	{
		"location": "Parkade P2",
		"scenario": "You call maintenance and ask for someone to help get the lights back on in the parkade. Time to head upstairs - do you take the elevator or the stairs?",
		"button1": "Elevator.",
		"button2": "Stairs.",
		"button3": "",
		"button4": "",
		"button1_dest": 5,
		"button2_dest": 6,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/0_dark_parkade.png",
		"achievement": "B",
	},
		# STORY 4
	{
		"location": "Parkade P2",
		"scenario": "Cars have headlights, and people have phones with flashlights, right? No need to worry about these lights right now. Time to head upstairs - do you take the elevator or the stairs?",
		"button1": "Elevator.",
		"button2": "Stairs.",
		"button3": "",
		"button4": "",
		"button1_dest": 5,
		"button2_dest": 6,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/0_dark_parkade.png",
		"achievement": "",
	},
		# STORY 5
	{
		"location": "Parkade P2 - Elevator Lobby",
		"scenario": "You press the elevator call button and wait. And wait. Waiting...",
		"button1": "Keep waiting...",
		"button2": "Take the stairs.",
		"button3": "",
		"button4": "",
		"button1_dest": 7,
		"button2_dest": 6,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/5_elevators.jpg",
		"achievement": "",
	},
		# STORY 6
	{
		"location": "Stairs (P2)",
		"scenario": "You enter the stairs and start the climb! You will reach the 4th floor in no time at all!",
		"button1": "Let's go!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 8,
		"button2_dest": 0,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/6_stairs.jpg",
		"achievement": "",
	},
		# STORY 7
	{
		"location": "Maybe purgatory, but it looks like the Elevator Lobby on P2",
		"scenario": "Yup, anyday now this elevator is going to arrive and everything is going to be ok.",
		"button1": "Keep waiting...",
		"button2": "Take the stairs",
		"button3": "",
		"button4": "",
		"button1_dest": 7,
		"button2_dest": 6,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/5_elevators.jpg",
		"achievement": "",
	},
		# STORY 8
	{
		"location": "Stairs (Level 2)",
		"scenario": "You're making your way up the stairs when you reach the landing for level 2. Your path is blocked by Heather and James discussing the on-going crisis of identifying the milk carton culprit! At first you are confused, but then you remember that Heather and James have brought this up before. Who keeps opening the milk carton incorrectly? Is it on purpose? Is it the milk carton's fault? How do we catch them in the act? What do you do?",
		"button1": "Join the conversation - This is important!",
		"button2": "Ask them to let you through.",
		"button3": "Push your way through.",
		"button4": "",
		"button1_dest": 26,
		"button2_dest": 9, 
		"button3_dest": 31,
		"button4_dest": 0,
		"image": "res://images/heatherjames.jpg",
		"achievement": "",
	},
		# STORY 9
	{
		"location": "Stairs (Level 2)",
		"scenario": "You nicely ask if Heather and James can step aside, but they are so deep into their discussion that they can't hear you. What now...",
		"button1": "Go through the adjacent door to level 2 and head to the other stairwell.",
		"button2": "Join the conversation. Scream out: 'THE CULPRIT MUST BE CAUGHT!'",
		"button3": "Push your way through.",
		"button4": "",
		"button1_dest": 10,
		"button2_dest": 26, 
		"button3_dest": 31,
		"button4_dest": 0,
		"image": "res://images/heatherjames.jpg",
		"achievement": "",
	},
		# STORY 10
	{
		"location": "Level 2 - Reception",
		"scenario": "You head to reception with hopes of getting to the other stairwell. No one can stop you now...",
		"button1": "Let's go!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 11,
		"button2_dest": 0,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/reception.jpg",
		"achievement": "",
	},
		# STORY 11
	{
		"location": "Level 2 - Reception",
		"scenario": "Luke pops out of the mechanical room! 'Hey Britt - there's a funny odour in the building? Do you smell that?' he says.",
		"button1": "I do! Let's check it out.",
		"button2": "Thanks for letting me know - I'll check it out later.",
		"button3": "Any idea what the cause is?",
		"button4": "",
		"button1_dest": 12,
		"button2_dest": 18,
		"button3_dest": 13,
		"button4_dest": 0,
		"image": "res://images/luke.jpg",
		"achievement": "",
	},
		# STORY 12
	{
		"location": "Level 2 - Mechanical Room",
		"scenario": "You go in the mechanical room and definitely notice an odour. But, there's something familiar and strange about it. It smells like... curry? You notice a small white plastic bag in the corner.",
		"button1": "Open the bag.",
		"button2": "Ask Luke, 'Did you go to Indian Fusion recently?'",
		"button3": "I don't want to know anymore. This is too strange, take me to level 4.",
		"button4": "",
		"button1_dest": 14,
		"button2_dest": 15,
		"button3_dest": 18,
		"button4_dest": 0,
		"image": "res://images/mech.jpg",
		"achievement": "",
	},
		# STORY 13
	{
		"location": "Level 2 - Reception",
		"scenario": "Luke says he doesn't know the cause, but suddenly feels hungry.",
		"button1": "Ooookay... Let's check the mechanical room?",
		"button2": "This is weird, I'm out of here. Take me to level 4.",
		"button3": "",
		"button4": "",
		"button1_dest": 12,
		"button2_dest": 18,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/luke.jpg",
		"achievement": "",
	},
		# STORY 14
	{
		"location": "Level 2 - Mechanical Room",
		"scenario": "You approach the bag. The smell is getting stronger. You open the bag, and see a curry lunch special!",
		"button1": "Luke?",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 15,
		"button2_dest": 0,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/mech.jpg",
		"achievement": "",
	},
		# STORY 15
	{
		"location": "Level 2 - Mechanical Room",
		"scenario": "Luke: 'OH! Right. I came here yesterday after lunch to check on the VFDs, must have left my lunch down here. I'll take that.'",
		"button1": "Give Luke his lunch and get back to your day.",
		"button2": "Throw the lunch on the ground!",
		"button3": "",
		"button4": "",
		"button1_dest": 16,
		"button2_dest": 17,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/luke2.jpg",
		"achievement": "",
	},
		# STORY 16
	{
		"location": "Level 2 - Mechanical Room",
		"scenario": "Luke: 'Thanks!' You head off to the other stairwell and continue to the 4th floor.",
		"button1": "Let's go!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 18,
		"button2_dest": 0,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/luke2.jpg",
		"achievement": "C",
	},
		# STORY 17
	{
		"location": "Level 2 - Mechanical Room",
		"scenario": "Luke: 'RUDE!' You head off to the other stairwell and continue to the 4th floor.",
		"button1": "Let's go!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 18,
		"button2_dest": 0,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/luke2.jpg",
		"achievement": "D",
	},
		# STORY 18
	{
		"location": "Level 4 - Outside F&P",
		"scenario": "What a morning, but you're almost at your desk. There is surely nothing else that can interrupt this day.",
		"button1": "Let's go!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 19,
		"button2_dest": 0,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/4th_floor.jpg",
		"achievement": "",
	},
		# STORY 19
	{
		"location": "Level 4 - Outside F&P",
		"scenario": "'Hey Britt! Happy Birthday... I have a favor to ask you.'",
		"button1": "Hey Mike - what do you need?",
		"button2": "Oh please no...",
		"button3": "I... can't do this right now. Talk to me later.",
		"button4": "",
		"button1_dest": 20,
		"button2_dest": 20,
		"button3_dest": 25,
		"button4_dest": 0,
		"image": "res://images/mike.jpg",
		"achievement": "",
	},
		# STORY 20
	{
		"location": "Level 4 - Outside F&P",
		"scenario": "'It's the strangest thing, but I cannot find my fob!' says Mike.",
		"button1": "Again?",
		"button2": "Do you need the loser fob?",
		"button3": "",
		"button4": "",
		"button1_dest": 21,
		"button2_dest": 24,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/mike.jpg",
		"achievement": "",
	},
		# STORY 21
	{
		"location": "Level 4 - Outside F&P",
		"scenario": "'This time I have a good excuse. I saw Heather and James going on about this 'Milk Culprit' thing again so I ran past them, but I must have dropped it in the process,' says Mike.",
		"button1": "You ran from them?",
		"button2": "Let's go get the loser fob.",
		"button3": "",
		"button4": "",
		"button1_dest": 22,
		"button2_dest": 23,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/mike.jpg",
		"achievement": "",
	},
		# STORY 22
	{
		"location": "Level 4 - Outside F&P",
		"scenario": "Of course I ran! Have you ever engaged them in that conversation? It goes nowhere!",
		"button1": "Sadly, I have.",
		"button2": "Actually, I ran too.",
		"button3": "",
		"button4": "",
		"button1_dest": 23,
		"button2_dest": 23,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/mike.jpg",
		"achievement": "",
	},
		# STORY 23
	{
		"location": "Facilities & Planning",
		"scenario": "You take Mike into F&P and get the infamous loser fob. Such a simple device, but it has saved many from the perils of waiting to hijack a ride with others in the elevator. You look ahead and see your desk. You made it! Now to sit in that sweet, sweet chair...",
		"button1": "Take a seat.",
		"button2": "Run to that chair before anyone else can interrupt you!",
		"button3": "",
		"button4": "",
		"button1_dest": 35,
		"button2_dest": 35,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/fp.jpg",
		"achievement": "E",
	},
		# STORY 24
	{
		"location": "Level 4 - Outside F&P",
		"scenario": "Mike: 'Does it have to be called the loser fob?'",
		"button1": "Yes.",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 23,
		"button2_dest": 0,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/mike.jpg",
		"achievement": "",
	},
		# STORY 25
	{
		"location": "Facilities & Planning",
		"scenario": "You walk past Mike and look ahead. There it is: your desk. You made it! Now to sit in that sweet, sweet chair...",
		"button1": "Take a seat.",
		"button2": "Run to that chair before anyone else can interrupt you!",
		"button3": "",
		"button4": "",
		"button1_dest": 35,
		"button2_dest": 35,
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/fp.jpg",
		"achievement": "",
	},
		# STORY 26
	{
		"location": "Stairs (Level 2)",
		"scenario": "You join the conversation in the middle of Heather and James plotting a plan to catch the culprit. They feel they should invite everyone on the 4th floor together, give each person a carton of milk to open, and watch the results. They both stare at you to see if you agree. How do you respond?",
		"button1": "Such a flawless idea - I see no issues with this at all!",
		"button2": "Won't this waste a lot of milk?",
		"button3": "Is this 'milk thing' really a big deal?",
		"button4": "",
		"button1_dest": 27,
		"button2_dest": 28, 
		"button3_dest": 29,
		"button4_dest": 0,
		"image": "res://images/heatherjames.jpg",
		"achievement": "",
	},
		# STORY 27
	{
		"location": "Stairs (Level 2)",
		"scenario": "Their eyes fill with a strange joy. 'It is,' they proclaim. 'Let's get the milk from other floors and prepare the trap! We can do this at your Birthday party!' They run off up the stairs and clear a path.",
		"button1": "Continue to the fourth floor!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 30,
		"button2_dest": 0, 
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/8_stairs.jpg",
		"achievement": "",
	},
		# STORY 28
	{
		"location": "Stairs (Level 2)",
		"scenario": "Their eyes fill with confusion. 'But, think of all the milk that is wasted when it leaks out of the incorrectly opened carton!' They jump back into their conversation, and it looks like you will be unable to get their attention again.",
		"button1": "Push through them!",
		"button2": "Go through the adjacent door to level 2 and head to the other stairwell.",
		"button3": "",
		"button4": "",
		"button1_dest": 31,
		"button2_dest": 10, 
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/heatherjames.jpg",
		"achievement": "",
	},
		# STORY 29
	{
		"location": "Stairs (Level 2)",
		"scenario": "Their eyes fill with confusion. 'Is this a big deal? IT'S A HUGE DEAL!' they shout. Their conversation starts again and it looks like you will be unable to get their attention again.",
		"button1": "Push through them!",
		"button2": "Go through the adjacent door to level 2 and head to the other stairwell.",
		"button3": "",
		"button4": "",
		"button1_dest": 31,
		"button2_dest": 10, 
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/heatherjames.jpg",
		"achievement": "",
	},
		# STORY 30
	{
		"location": "Stairs (Level 3)",
		"scenario": "You continue up the stairs when suddenly you feel something hit the tip of your shoe and slide across the floor. You look down and notice a USB stick on the ground. What do you do?",
		"button1": "Ignore it - this is not mine and someone else may come look for it.",
		"button2": "Take it. I can see if it's empty or not on my computer and give it to the correct person.",
		"button3": "Pick it up and take it to ICT.",
		"button4": "",
		"button1_dest": 32,
		"button2_dest": 34, 
		"button3_dest": 33,
		"button4_dest": 0,
		"image": "res://images/usb.jpg",
		"achievement": "",
	},
			# STORY 31
	{
		"location": "Stairs (Level 2)",
		"scenario": "You can't take this anymore! You step back, get in a sprinter's starting stance, then push through at full speed. *BAM* You're through them and on your way to the fourth floor! You hear Heather and James saying that you must be the milk culprit.",
		"button1": "Let's go!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 30,
		"button2_dest": 0, 
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/8_stairs.jpg",
		"achievement": "G",
	},
		# STORY 32
	{
		"location": "Stairs (Level 3)",
		"scenario": "You kick the USB stick off the side of the stairs and decide to keep going. You briefly ponder your decision and wonder if the recent ICT security training would approve of your choice. Then again, it's your birthday and you can do what you want. Off to the fourth floor!",
		"button1": "Let's go!",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 18,
		"button2_dest": 0, 
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/8_stairs.jpg",
		"achievement": "H",
	},
		# STORY 33
	{
		"location": "Stairs (Level 3)",
		"scenario": "You grab the USB stick and head straight to ICT. You're rewarded with cheers from the entire department as you hand in the security threat. You feel proud! They want to celebrate your decision, and you invite them to your birthday party later this morning.",
		"button1": "Woohoo! Let's continue to the fourth floor.",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 18,
		"button2_dest": 0, 
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/8_stairs.jpg",
		"achievement": "I",
	},
		# STORY 34
	{
		"location": "Stairs (Level 3)",
		"scenario": "You grab the USB stick and put it in your pocket. You can check the contents later and make sure it goes to the right person. This USB stick could contain sensitive or confidential information that should not be left out for anyone to grab!",
		"button1": "Continue to the fourth floor.",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": 18,
		"button2_dest": 0, 
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/8_stairs.jpg",
		"achievement": "J",
	},
		# STORY 35
	{
		"location": "Your Desk",
		"scenario": "Finally, you made it. You take a seat at your desk and close your eyes. In the brief journey from parkade to fourth floor office, you encountered a lot. You have a few things to do before your party starts, and you should reflect on your day...",
		"button1": "Reflect on the outcomes of my choices...",
		"button2": "",
		"button3": "",
		"button4": "",
		"button1_dest": "end",
		"button2_dest": 0, 
		"button3_dest": 0,
		"button4_dest": 0,
		"image": "res://images/desk.jpg",
		"achievement": "",
	},
]

func _ready():
	display_story(stories[0])


func display_story(story):
	location_text.text = story["location"]
	scenario.text = story["scenario"]
	image.texture = load(story["image"])
	button1.text = story["button1"]
	button2.text = story["button2"]
	button3.text = story["button3"]
	button4.text = story["button4"]
	button1_dest = story["button1_dest"]
	button2_dest = story["button2_dest"]
	button3_dest = story["button3_dest"]
	button4_dest = story["button4_dest"]
	Globals.Achievements += story["achievement"]
	show_or_hide_buttons()


func show_or_hide_buttons():
	button1.visible = false if button1.text == "" else true
	button2.visible = false if button2.text == "" else true
	button3.visible = false if button3.text == "" else true
	button4.visible = false if button4.text == "" else true


func go_to_end_screen():
	get_tree().change_scene("res://End.tscn")


func _on_Button1_button_down():
	if str(button1_dest) == "end":
		go_to_end_screen()
	else:
		display_story(stories[button1_dest])


func _on_Button2_button_down():
	if str(button2_dest) == "end":
		go_to_end_screen()
	else:
		display_story(stories[button2_dest])


func _on_Button3_button_down():
	if str(button3_dest) == "end":
		go_to_end_screen()
	else:
		display_story(stories[button3_dest])


func _on_Button4_button_down():
	if str(button4_dest) == "end":
		go_to_end_screen()
	else:
		display_story(stories[button4_dest])
```