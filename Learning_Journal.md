# LEARNING JOURNAL

##Component Package One- 3D Player Controller

When creating the general "PlayerController" script, I wanted to move the player object left, right, forward and backward by applying forces to the rigidbody. However, I want to do this by calling the function "MovePlayer()" when the keys are inputted. I decided to place the calling of this function in the "Update()" function. This did not work. I also tried to call it in the "MyInput()" function, however this failed as well.
