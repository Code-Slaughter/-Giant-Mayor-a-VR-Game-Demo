# Giant Mayor VR Game

This Game is designed as final project for EPFL master course: CS-444 "Virtual Reality"

Due to the limitation of github, I cannot upload the whole code files :(

Here is the link for you to see the final presentation of this game: [CLICK ME](https://www.youtube.com/watch?v=BPuymwXoFCc)

## Game synopsis
The “Giant Mayor” is in an evaluation period, and his/her duty is to ensure the
prosperity of the city. The player needs to complete several tasks to become a
beloved Mayor. There are mainly three tasks: catch dragons and send them back to
their world via portals, save people from fire and send him/her to hospital, and kill the
giant monster using a lightsaber.

![image](https://user-images.githubusercontent.com/76023123/172089447-4f9e086a-6805-489f-9e20-54069c794fee.png)
![image](https://user-images.githubusercontent.com/76023123/172089462-ea5c2fa3-a3c8-4895-aa2e-0063cdb938f7.png)

## Interactions
- Commands and Cheat Codes

  ![image](https://user-images.githubusercontent.com/76023123/172089521-cf645434-dda1-43d8-b693-5a0cebebf847.png)
  
  In the part of processing grabbing and remote grabbing, considering the change of the button state, we analyzed the function table corresponding to the current frame state and the previous frame state in each case.
  More specifically, we define three different states : grabbing, remote grabbing and none state. The table is shown below:
  
  ![image](https://user-images.githubusercontent.com/76023123/172089582-734b1dfa-80c9-4738-b8f7-23c1f7654340.png)

- Grab

  - **Command**: Press "SecondaryIndexTrigger" and "SecondaryHandTrigger" at the same time
  - **Function**: Grab an object.
  - **Implementation**: Detect the grab state of each frame, call the attach and detach functions according to the above state function table to realize the corresponding functions.

- Throwing

  - **Command**: Keep grabbing an object, swing your arm then release all buttons.
  - **Function**: Throw the grabbed object.
  - **Implementation**: When the button state shows that the object needs to be detached, detect the position difference between the previous frame and the current frame, and then calculate the initial velocity that the object should have.

- Filling a Container

  - **Command**: Keep grabbing an object, put it on top of the container then release.
  - **Function**: Put an object into the container.
  - **Implementation**: When the object is placed in the box, set the object's parent to the current container and useGravity in its rigid property to false.

- Swing and Hit

  - **Command**: Press "X" and swing your arm.  
  - **Function**: Swing your lightsaber and hit the monster.  
  - **Implementation**: First, press X to issue a lightsaber. When hitting a monster, the program will calculate the current speed of swinging the lightsaber, and set the damage to the monster according to the speed.

- Alternate Grab

  - **Command**: Press "SecondaryHandTrigger" to search objects then press "SecondaryIndexTrigger".
  - **Function**: Grab an object in the distance.
  - **Implementation**: Press "SecondaryHandTrigger" to fire a ray for selecting the object you want to grab. After selecting, press "SecondaryIndexTrigger", which will modify the position of the object to be close to the front of the controller. Then execute the attach function to grab the object.
  
- Alternate Locomotion

  - **Command**: Press "PrimaryHandTrigger".
  - **Function**: Move forward continuously for 20 meters in the player's looking-at direction.
  - **Implementation**: When the button is pressed, we do linear interpolation between the current player position and target position that is 20 meters away. Player will only dash one time even when the button is continuously pressed.
  
## Other features
- Cheat sheet
  
  A panel will appear in front of and facing the player when pressing Y in the scene. There is the tutorial on the left, the minimap and todo list on the right. Whenever a task is completed, a green tick will appear on the corresponding item.

- Minimap
  
  There is a minimap in the upper right corner of the cheat sheet. It shows the contents of a camera following the player high in the sky. Player and dragon icons are also displayed on the map, while invisible from the OVR camera so they don’t influence the main view.

- NPC patroling
  
  We used the NavMeshAgent component and baked the navigation area. The CitizenController script will periodically update the walkable destinations within a certain range. So citizens can walk randomly on the sidewalk.

- Animation
  
  We added Animator components to control the animations that come with the model. Includes animations of people walking in the scene, dragons flying low, and the monster being hit and dying.

- Particle Effect
  
  There are three portals for dragons and one portal for putting baskets. When the dragons and basket collide with their corresponding portals, particle effects will be triggered to give users proper feedback.

- Sound
  
  The game has a continuous background music and sound effects triggered by certain events, implemented with Audio Source components and controlled by code on each related

- Vibration
  
  When hitting the monster with the lightsaber, the left controller will vibrate.


## Play test and feedback
In the playtesting session, 12 users tested our game and gave constructive and
friendly comments. Big smiles appeared on their faces when testing our game.

One of them suggested that we can add vertical fences to the basket(container for
saving people) to avoid people falling out, and we took this suggestion in our final
version of the game.

Another user argued that all of our tasks happen on the same street in the scene,
which is a little bit overwhelming. Therefore we put the giant monster task on another
street to make the task more scattering.

People also mentioned that they have trouble finding the portal for saving people. To
address this problem we put several information boards in the scene to clearly show
the portal position.
  
We want to express our sincere thanks to all the testers! Their suggestions are really
helpful and important to us. We thank them all :)
