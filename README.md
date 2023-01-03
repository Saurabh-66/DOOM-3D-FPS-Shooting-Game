# DOOM-3D-FPS-Shooting-Game
DOOM is a 3 dimensional first person shooter (FPS) shooting game which uses raycasting algorithm to generate a pseudo 3D environment and pathfinding algorithm for smart player enemy interaction. It is built using Pygame module in Python and takes advantage of the raycasting algorithm to make a 3D gameplay despite not being a 3D game engine unlike Unity, Unreal, Godot and others that are available in the market.

Below is the demonstration of the gameplay.

![Gameplay](/photos/gameplay_1.gif)

## Table of Contents

- [Player movement](#player-movement)
- [Raycasting Algorithm](#raycasting-algorithm)
- [Static and Animated Sprites (decorations)](#static-and-animated-sprites-decorations)
- [Weapon and shooting animation](#weapon-and-shooting-animation)
- [Player Enemy interaction (Pathfinding)](#player-enemy-interaction-pathfinding)
- [Enemies](#enemies)
- [Final Gameplay](#final-gameplay)

### Player movement

Initially we built the player movements, which is based on any classic FPS shooting game, WASD keys for front, back, left and right directions respectively and left, right arrow key or mouse for the rotation of the player at that particular position.

Below is the implementation of the same (viewed in 2D perspective to confirm movement in correct irection along with wall collisions, the green dot is the player and the yellow line is the line of sight of the player).

![Player movement](/photos/player_1.gif)

### Raycasting algorithm

In raycasting algorithm we cast a fixed number of rays in the field of view of the player, if field of view (FOV) angle is **X**, then the area visible to the player at a particular time would be equal to ***player's current angle (line of sight) - half of FOV angle (X/2)*** to ***player's current angle (line of sight) + half of FOV angle (X/2)***. The rays will be cast in this particular region till they meet an obstacle (wall) which will give the depth perspective of that particular point wrt the player. 

Raycasting algorithm visual representation in 2D perspective is shown below (rays cannot pass the walls as they are obstacles).

![Raycasting algorithm](/photos/raycast_1.gif)

Once we get the collision point of the rays within the field of view (FOV) of the player, we can use it to generate a pseudo 3D perspective as shown below.

![Raycasting algorithm](/photos/raycast_2.gif)

The current pseudo 3D looks even more realistic if we apply shaders to it, i.e. darkness of a particular point based on the distance of the collision point from the player (the farther the point, the darker is the image). 

![Raycasting algorithm](/photos/raycast_3.gif)

Now that we have obtained a pseudo 3D environment for our gameplay, we can add more life to it and make it look realistic by adding textures to the walls, adding a background and floor color.

![Raycasting algorithm](/photos/raycast_4.gif)

### Static and Animated Sprites (decorations)

In order to make the game more beautiful we add static and animated sprites to make the game environment more realistic. The animated sprites are nothing but a collection of static images which are displayed on the screen faster than the human eye's persistence of vision which makes it look like it's a moving object, this can be achieved if the frame rate at which the images are displayed is faster than the persistence of vision of human eye, eg. 30 frames per second (fps), 60 fps, etc.

Static and animated sprites added into the game environment.

<img src="/photos/assets_1.png" width=15%>
<img src="/photos/assets_2.gif" width=15%>
<img src="/photos/assets_3.gif" width=15%>

Game environment along with the static and animated sprite decorations.

![Gameplay](/photos/gameplay_2.gif)

### Weapon and shooting animation

Now the game environment is achieved so we need to add a weapon and its shooting animation so that the player can interact with the enemies in the game. The shooting animation is triggered using the left mouse button which is accompanied with a waiting time for the recoil animation to get completed. Once the fire animation is complete the weapon is ready to shoot again.

![Weapon](/photos/weapon_1.gif)

### Player Enemy interaction (Pathfinding)

The first idea is that the enemy is follow the player once the player is in line of sight and in a particular radius of the enemy. The enemy will try to follow the player along the line connecting the enemy and the player current position keeping in mind the game environment constraints that enemy cannot move outside the game screen and enemy cannot move through walls.

The implementation of this idea is given via the visual representation below (2D perspective to visualize the interaction properly).

![Player Enemy interaction](/photos/player_enemy_1.gif)

Drawback of the above method is that the enemy tries to follow the player along the line connecting the enemy and the player, but when the player moves behind the wall the enemy tries to follow the player along the line through the wall but because of the presence of the wall is unable to do so, which looks stupid as we want our enemy to be smart and be able to navigate through the obstacles to reach the player through the shortest path possible. 

The enemy should be able to determine a work around to reach the player once encountered with walls and this can be achieved via a pathfinding algorithm called breadth first search (BFS). Below shows the working of the algorithm where the enemy follows the player bypassing obstacles via path which is the shortest to reach the player. 

![Player Enemy interaction](/photos/player_enemy_2.gif)

Now lets introduce more enemies in the playing arena and look at the smart enemy following strategy where they are able to trap the player from time to time to inflict maximum damage to the player.

![Player Enemy interaction](/photos/player_enemy_3.gif)

### Enemies

Now lets add different enemy characters to make the gameplay more fun and interesting. All enemy characters have different walk, attack, death, etc. animations and have different statistics regarding health, damage amount and radius and various other attributes.

#### Soldier

![Soldier](/photos/soldier_1.gif)
![Soldier](/photos/soldier_2.gif)
![Soldier](/photos/soldier_3.gif)

#### Caco Demon

![Caco Demon](/photos/cacodemon_1.gif)
![Caco Demon](/photos/cacodemon_2.gif)
![Caco Demon](/photos/cacodemon_3.gif)

#### Cyber Demon

![Cyber Demon](/photos/cyberdemon_1.gif)
![Cyber Demon](/photos/cyberdemon_2.gif)
![Cyber Demon](/photos/cyberdemon_3.gif)

### Final Gameplay

Adding minute details like damage, health percentage and end screen eventually leads us to the final gameplay as seen below.

![Gameplay](/photos/gameplay_1.gif)
