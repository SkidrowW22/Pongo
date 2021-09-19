# Pongo

Developed with Unreal Engine 4 using blueprints

This is my first Unreal Engine 4 project. It is a very simple ping pong game with a few important details/mechanics. One game lasts till 5 goals, you play against an AI (*AI it's a big word for a few linear and very straighforward commands and instructions*) opponent. All the logic part of the project was made with blueprints, no code. 

The reason I made this project was to test my newly acquired knowledges in Unreal Engine 4 blueprints and the best way to use them is to make something simple but with working logic from the beginning till the end. It's better to start with something little but working than a big, special idea which requires tons of hours, people and knowledge.

At the beginning i'll throw some screenshots of logic behind the game with explanation and at the end will be a short video with demonstration of the gameplay. All blueprint files you can find in the master branch/Content/Blueprints. To open a blueprint you just need to download it and move it to an opened project in Unreal Engine 4.

## Blueprints

Here I'm using impulse on Sphere (*which is a static mesh, physic object in the world*), this logic was made in Pball blueprint (*ping pong ball*).
![3](https://user-images.githubusercontent.com/90534698/133913442-bf65763f-c632-48c2-8432-ebecf55a8e41.png)

Next we need the logic to spawn the ball in world. The blueprint is basically an invisible actor with an attached arrow which serves as spawn point for the ball. All the logic is stored in custom event SpawnNextB so it can be called in other blueprints. The ball spawnes at the arrow location and rotation (*with transform node we check and pass the location of arrow point to the pball*)  with a delay of 1 second.
![4](https://user-images.githubusercontent.com/90534698/133913499-bb08fe9d-bb4b-4ed2-a182-450f8163eb5f.png)

Here is the logic for player paddle. We just multiply the axis value (*which is 1*) with a variable speed and pass this to makevector node which moves the paddle on x axis. At the final we add the result to the impulse node which uses the paddle as target.
![5](https://user-images.githubusercontent.com/90534698/133913907-603e127a-939e-462f-9800-d05e45160725.png)

The lefttrigger and righttrigger blueprints are trigger boxes which are used in another blueprint.

![1](https://user-images.githubusercontent.com/90534698/133913386-746ab805-06e6-4d9f-837e-a7cb66b748cc.png)
![2](https://user-images.githubusercontent.com/90534698/133913387-b8236632-de2b-40fc-bf35-d398ac8666a9.png)
