# Pongo

Developed with Unreal Engine 4 using blueprints

This is my first Unreal Engine 4 project. It is a very simple ping pong game with a few important details/mechanics. One game lasts till 5 goals, you play against an AI (*AI it's a big word for a few linear and very straighforward commands and instructions*) opponent. All the logic part of the project was made with blueprints, no code. 

The reason I made this project was to test my newly acquired knowledges in Unreal Engine 4 blueprints and the best way to use them is to make something simple but with working logic from the beginning till the end. It's better to start with something little but working than a big, special idea which requires tons of hours, people and knowledge. I didn't create the Start Game Menu, Pause Menu or Win/Lose Menu because I wanted to focus more on core gameplay and it's mechanics.

At the beginning i'll throw some screenshots of logic behind the game with explanation and at the end will be a short video with demonstration of the gameplay. All blueprint files you can find in the master branch/Content/Blueprints. To open a blueprint you just need to download it and move it to an opened project in Unreal Engine 4.

## Blueprints

Here I'm using impulse on Sphere (*which is a static mesh, physic object in the world*), this logic was made in Pball blueprint (*ping pong ball*).
![3](https://user-images.githubusercontent.com/90534698/133913442-bf65763f-c632-48c2-8432-ebecf55a8e41.png)

Next we need the logic to spawn the ball in world. The blueprint is basically an invisible actor with an attached arrow which serves as spawn point for the ball. All the logic is stored in custom event SpawnNextB so it can be called in other blueprints. The ball spawnes at the arrow location and rotation (*with transform node we check and pass the location of arrow point to the pball*)  with a delay of 1 second.
![4](https://user-images.githubusercontent.com/90534698/133913499-bb08fe9d-bb4b-4ed2-a182-450f8163eb5f.png)

Here is the logic for player paddle. We just multiply the axis value (*which is 1*) with a variable speed and pass this to makevector node which moves the paddle on x axis. At the final we add the result to the impulse node which uses the paddle as target.
![5](https://user-images.githubusercontent.com/90534698/133913907-603e127a-939e-462f-9800-d05e45160725.png)

The lefttrigger and righttrigger blueprints are trigger boxes which are used in Pball blueprint.

Here is the scorring system. I used Event actorbeginoverlap node and cast it to lefttrigger and rightrigger, in that way all logic is scripted in pball blueprint where I can freely acces the ping pong ball and trigger boxes. The score is stored in PongPawn, the EventActorBeginOverlap is executed through a multigate node which fires every tick and in loop the whole logic behind LeftTrigger and RightTrigger. Also, the multigate resets everytime when one of the logic is executed, this is very important for the score because otherwise the logic will fire in order of their sequence number, which is not correct. 
![1](https://user-images.githubusercontent.com/90534698/133913386-746ab805-06e6-4d9f-837e-a7cb66b748cc.png)
![2](https://user-images.githubusercontent.com/90534698/133913387-b8236632-de2b-40fc-bf35-d398ac8666a9.png)

Here we have the AI logic for the enemy paddle. In the first node group the variable Tick Interval is set to 0.1 which means that the logic bellow will fire only 10 times per second which is better at memory saving than the default value of tick interval at 60 times per second. In the below logic we simply find the relative location of the ball and if this is valid (*the ball is in the world, not destroyed*) we pass the information to the newly created function Move.
![11](https://user-images.githubusercontent.com/90534698/133947323-b4bf7934-da8b-479b-8924-1b75b9c150d9.png)
The logic behind paddle movement is quite simple. The cube (*which is the enemy paddle*) moves only on x axis which is the location variable from our previous note, so basically the paddle follows the ball movement only on x axis. Also, the clamp node allows the paddle to move only in the given coordinates on x axis so it won't move out of the map boundaries. The variable Mtime controlls how fast the paddle will react to the ball movements.
![7](https://user-images.githubusercontent.com/90534698/133947000-0f58f68b-2259-4adf-a249-2b3d4a8febf4.png)

For the hud we have only 2 text blocks with two variables binded to them.
![8](https://user-images.githubusercontent.com/90534698/133947232-bdd63ae4-6d9f-4e5d-a2b9-31a01e1d7974.png)
![9](https://user-images.githubusercontent.com/90534698/133947250-bfd7575e-c106-4986-a7c7-bcd8d01199a9.png)
And here we assign the score variables to the hud text blocks and store them in pong pawn.
![10](https://user-images.githubusercontent.com/90534698/133947290-1383adf3-7e52-42ac-9922-48786b8fbfa0.png)

Now, here's a demonstration of gameplay. In first video I made the enemy is very easy to beat by tweaking Mtime variable which is paddle movement reaction to the ball location. In the second one I made him almost impossible to beat.

https://youtu.be/yOFsObtzxR0

https://youtu.be/GllMJjtHrV4
