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
