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

![Screenshot 2023-01-31 135420](https://user-images.githubusercontent.com/114989045/215807827-53010042-2c8d-4ad0-bbd5-311880483c57.png)

![Screenshot 2022-10-18 115531](https://user-images.githubusercontent.com/114989045/215807872-35b80725-7fd3-4b44-870f-9450df23c03f.png)

As shown above, I changed the nudge room float of 0.2f to 0.51 by testing it in Unity.
