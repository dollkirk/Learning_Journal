# LEARNING JOURNAL

## Component Package One- 3D Player Controller


#### PROBLEM:
When creating the general "PlayerController" script, I wanted to move the player object left, right, forward and backward by applying forces to the rigidbody. However, I want to do this by calling the function "MovePlayer()" when the keys are inputted. I decided to place the calling of this function in the "Update()" function. This did not work. I also tried to call it in the "MyInput()" function, however this failed as well.

#### SOLUTION:

![Screenshot 2022-10-18 115531](https://user-images.githubusercontent.com/114989045/215777158-be9a8f9b-ddfd-4aa7-8978-33034f913995.png)

As shown above, I decided to comment out the "MovePlayer()" function for now and placed the line of code that applies the forces to the player's rigidbody in the "MyInput()" function. During this process, I realised that the player object would have a force applied horizontally, however, not vertically. This was due to a typo error when putting in the "AddForce" coordinates.
