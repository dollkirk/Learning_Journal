# LEARNING JOURNAL

## Component Package One - 3D Player Controller


#### PROBLEM:
When creating the general "PlayerController" script, I wanted to move the player object left, right, forward and backward by applying forces to the rigidbody. However, I want to do this by calling the function "MovePlayer()" when the keys are inputted. I decided to place the calling of this function in the "Update()" function. This did not work. I also tried to call it in the "MyInput()" function, however this failed as well.

#### SOLUTION:

![Screenshot 2022-10-18 115531](https://user-images.githubusercontent.com/114989045/215777158-be9a8f9b-ddfd-4aa7-8978-33034f913995.png)


As shown above, I decided to comment out the "MovePlayer()" function for now and placed the line of code that applies the forces to the player's rigidbody in the "MyInput()" function. During this process, I realised that the player object would have a force applied horizontally, however, not vertically. This was due to a typo error when putting in the "AddForce" coordinates.

#### PROBLEM:
Now that the forces were being applied to the player, I realised that it was knocking the player object over instead of sliding it over to the side. This meant I needed to somehow freeze the player object's rotation in all of the axes.

#### SOLUTION:

![Screenshot 2023-01-31 135420](https://user-images.githubusercontent.com/114989045/215779295-192c348c-3768-4531-adbe-bdb68646f84f.png)


Using the rigidbody component on the player object, I freezed the rotations.


#### PROBLEM:
The "Jump()" function was no longer working after creating a way to check for if the player object is grounded (touching the plane with the layer "Ground".

#### SOLUTION:
When checking if the player object is grounded, I am using a raycast to point downwards originating at the distance of half the player objects height down to the bottom of the player object (plus 0.2f to give nudge room). The layer it is looking for is called "Grounded" and the plane I have created has that layer assigned. 
To check if this was working, I used "Debug.Log" to display if the boolean variable "grounded" is becoming set to equal true when the player object is just placed on the plane. This displayed in the console that the value of "grounded" was actually false at the start. Therefore, the raycast was not hitting the ground at the start.

![Screenshot 2023-01-31 154513](https://user-images.githubusercontent.com/114989045/215807971-141fa5a1-5f3c-4f23-8257-3a9f8cacc6a5.png)


![Screenshot 2023-01-31 154526](https://user-images.githubusercontent.com/114989045/215808052-b4f4c77d-3433-4003-986e-2a70ed051195.png)


As shown above, I changed the nudge room float of 0.2f to 0.51 by testing it in Unity.

#### PROBLEM:
I wanted to create a double jump for my Player Controller script. First, I tried using a  nested if statement to call the function "Jump()" again when the space key is pressed again when the player object is not "grounded".

![Screenshot 2023-02-07 102736](https://user-images.githubusercontent.com/114989045/217223685-eac3d517-65a6-448a-ad29-547940a92261.png)


This did not work. Next, I tried a while loop to say whilst the player is not "grounded", check the if statement of if the space key is pressed. This did not work either.

#### SOLUTION:
I created two new private integer variables: "maximumJumps" equal to 2, and "currentJump" equal to 0. In the update function, I then needed to set "currentJump" equal to 0 when the player is "grounded" as the player shouldn't be able to double jump when grounded, only singular jump.

![Screenshot 2023-02-07 105124](https://user-images.githubusercontent.com/114989045/217227215-8767aae2-5a5b-40c8-a72c-f9da528eb705.png)


Next, I needed to edit the jump key input if statement in the "MyInput()" function. I changed the statement to if the player is "grounded" or if the number of "currentJump" is less than the number of "maximumJumps". I then incremented the value of "currentJump" whenever that if statement happens.

![Screenshot 2023-02-07 105150](https://user-images.githubusercontent.com/114989045/217228710-1bd2c9bb-6fa9-444b-8006-33f3bcdde626.png)


#### PROBLEM:
I created a new script called "PlayerPickup" to allow the player object to pick up certain interactable objects. I did this by creating 2 functions, "OnMouseDown()" and "OnMouseUp()". I then accessed the interactable object's rigidbody and set the gravity as false when "OnMouseDown()". I did the same in the "OnMouseUp()" function but set the gravity back to true. I also set the transform position of the interactable object equal to the same position of the empty child object named "Destination". This worked and allowed the player to pick up the interactable object, however, it did not update the "Destination" psotion when the player moved, and kept the interactable object in that same position.

#### SOLUTION:
I created a boolean variable named "MouseDown" and set it as true when "OnMouseDown()" was called, and set it as false when "OnMouseUp()" was called. Then I placed all of the transforms and Rigidbody code into an if statement in the update function as below:

![Screenshot 2023-02-07 131409](https://user-images.githubusercontent.com/114989045/217254632-f238d241-43d6-4db5-ac0c-74d4adf6167f.png)


#### PROBLEM:
I edited the "PlayerController" script to rotate the player object in the direction of where it is moving. This worked, however, when the player jumped, the player object would land and lay vertically face down.

#### SOLUTION:
I changed the if statement that was checking the player object's rigidbody velocity. I added that the player needed to be "grounded" and that the rigidbody velocity shouldbe equal to not(0, -1, 0) for it to happen.

![Screenshot 2023-02-13 124625](https://user-images.githubusercontent.com/114989045/218461304-55ea7117-7924-417c-88b0-b1b21cd8074a.png)


## Component Package Two - Platform movement/Respawn Checkpoints

#### PROBLEM:
I created two scripts called "MovingPlatformController" and "WayPoints". In the "WayPoints" script, it is keeping count of the waypoints of the moving platform path. The "MovingPlatformController" is moving the platform using transforms and "Lerp". I set two waypoints for the platform to move between and this works. However, I want the platform to rotate in the same rotation that the waypoints are in.

![Screenshot 2023-03-07 142622](https://user-images.githubusercontent.com/114989045/223452314-10f5f1cf-54b4-49f1-bfa0-2bb161cbb439.png)


#### SOLUTION:
I used "transform.rotation" and "Quarternion.Lerp" to rotate the platform in the same position as the waypoint that is next. This is shown below:

![Screenshot 2023-03-07 143154](https://user-images.githubusercontent.com/114989045/223452586-f2f4d431-73bf-4a35-ad68-a5c6779c24ab.png)

#### PROBLEM:
I realised that this component was too small, therefore, I wanted to create a respawn checkpoint system as well. I first found a tutorial online and created three scripts: "CheckpointController", "PlayerPos" and "RespawnCheckpoints". The tutorial was based on a 2D game and was therefore using Vector2.

#### SOLUTION:
This was an easy fix as I just replaced all Vector2 details to Vector3 for it to work in 3D.

#### PROBLEM:
I followed the tutorial step by step and found that the creator was using "UnityEngine.SceneManagement" to reload the scene everytime the player needed to respawn at the correct checkpoint. I just wanted the player to transform position back to the last checkpoint that was triggered.

#### SOLUTION:
In the script "PlayerPos", I edited the if statement checking for the correct key input in the "Update()" function. I deleted the scene management line of code which reloaded the scene everythime and replaced it with what is shown below:

![Screenshot 2023-03-18 210110](https://user-images.githubusercontent.com/114989045/226139887-0edba30a-fcb5-47c6-8d9f-8726580823a7.png)


## Component Package Three - Reset Area/Companions

#### PROBLEM:
I created a script called "ResetArea" that created an array and destroyed each object in that array when the player object collides with the area collider. I tried to use "Length" to find the maximum amount of objects in the array and to then destroy the objects by doing "Destroy(gameObjects[max])". However, this just destroyed the gameobject in the last position of the array.

#### SOLUTION:
I instead used "foreach" to do this as shown below:

![Screenshot 2023-02-14 124835](https://user-images.githubusercontent.com/114989045/218743298-487e6db0-241b-4f6d-8fc0-6ea538c8408c.png)

#### PROBLEM:
I realised that the method of resetting the area was inefficient for the functions I wanted to add: I wanted the objects to be AI and when the player collides with the AI, it follows just as it does in the Component Package One. Therefore, I needed to create a state machine to give the AI functions for when it is hostile and when it is a companion.

#### SOLUTION:
I created 5 new scripts to function as this state machine: "AIStateController", "AIState", "AIEnemySate" for when the AI is hostile, "AIEnemyMove" to move the AI in a patrol movement when it is in "AIEnemyState" and "AICompanionState" for when the player collides with the AI.

#### PROBLEM:
When setting the movement points for when the AI is in the "AIEnemyState" in the script "AIEnemyMove", I used an "OnTriggerEnter" function to say that when the AI collides with the points that have this script attached, the AI will move to the next point in the order of the points array. However, this did not work when tested in Unity.

#### SOLUTION:
I added a rigidbody component to the movement points in the array.

![Screenshot 2023-02-17 160207](https://user-images.githubusercontent.com/114989045/219703949-87f6bcc0-6694-4d08-b86a-519e70aac957.png)


#### PROBLEM:
I wanted to change the state back to the "AIEnemySate" script when it is in the "CompanionState" script and collides with a trigger death zone. I created a trigger function to check if the AI game object collides with the trigger with the tag "DeathZone". If it does, I then changed the state to the "enemyState". This worked, however, the AI was not going back to its patrol points.

![Screenshot 2023-02-21 104710](https://user-images.githubusercontent.com/114989045/220324337-f21a5b2c-9676-44cd-ae9e-46a17a8c3a5d.png)


#### SOLUTION:
I realised that the target points were being set in the "Start()" function. This meant I needed to set them again when the state changes back to "AIEnemyState". Therefore, i put the target transforms into this trigger function as shown below:

![Screenshot 2023-02-21 104735](https://user-images.githubusercontent.com/114989045/220324503-e6213ba9-295a-4ce1-8896-79330eb32d8f.png)

#### PROBLEM:
I created a script called "CompanionCount" and created a simple count system for everytime the player object collides with an object with the tag "AI" which are the companion objects. It then displays the number of companions collected with a Text Mesh Pro UI element. However, it counts the same object collision multiple times. I want it to only count the companions once.

![Screenshot 2023-03-07 111440](https://user-images.githubusercontent.com/114989045/223406860-f29bd898-dc25-479e-b9fd-0c39d8516d67.png)

#### SOLUTION:


## Component Package Four - Wind Cycle

#### PROBLEM:
I created a state machine using 5 scripts: "WindState", "WindStateController", ""WindOnState", "WindOffState" and "ObjectsAffectedByWind". I wanted this component to apply a force for a certain amount of time when the player object triggers it. Therefore, I needed to add a timer. 

![Screenshot 2023-02-28 114400](https://user-images.githubusercontent.com/114989045/221845420-4a03199a-709f-4bc6-bf61-b7bc2c0727e9.png)

As shown above, I created this if statement to use "Time.deltaTime" to count down when when the player hits the trigger. This worked the first time when the player triggers it, however, it wouldn't do it again after triggering it. I wanted it to iterate everytime the countdown finished and the player triggered it again.

#### SOLUTION:
I realised that as I had used a state machine to create this component, I needed to update the next state to the "offState" again after the "Destroyed" function that stops that current state.

![Screenshot 2023-02-28 114414](https://user-images.githubusercontent.com/114989045/221845618-3611d8d3-a963-4d1b-9e32-6052c81660bf.png)


#### PROBLEM:
Now that I had the states, the trigger and timer working, I needed the "WindOnState" to apply a force to all interactable objects in the scene. I tried to create a function called "ApplyForce()" in the "WindOnState" script, however, this did not work as I couldn't access the "GetComponent" in this script. This may have been because the "WindOnState" is using the "WindState" behaviour rather than the "MonoBehaviour" Unity provides.

#### SOLUTION:
I instead created the "ApplyForce()" function in the "WindStateController" script and called it in the "WindOnState" script as shown below:

![Screenshot 2023-02-28 122507](https://user-images.githubusercontent.com/114989045/221853664-59d655c2-25e3-43fd-aab6-d3647f74e008.png)

![Screenshot 2023-02-28 122454](https://user-images.githubusercontent.com/114989045/221853698-5f4b89ce-b383-44aa-a74c-6bbcb4f9aa63.png)


#### PROBLEM:
I wanted to make the wind direction cycle left to right constantly after every 5 seconds. I created this if statement in the "WindStateController" script in the "ApplyForce()" function:

![Screenshot 2023-02-28 133650](https://user-images.githubusercontent.com/114989045/221869971-93d03288-baf5-4efc-bb47-a18505bafb3a.png)

However, this did not loop the cycle as my component is using states and I would change the state from "WindOn" to "WindOff".

#### SOLUTION:
Therefore, I edited the "Update()" function where the timer counts down. I changed the states when the timer ran out and then immediately changed it back to the on state again:

![Screenshot 2023-02-28 133945](https://user-images.githubusercontent.com/114989045/221870667-85108115-ed93-4e4b-af16-678d230ce62a.png)


