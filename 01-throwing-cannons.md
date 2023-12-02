


https://github.com/jinyongnan810/UE5-learning/assets/29720903/a1c9997a-7691-4fed-a94d-d3775b261e1f


# Steps
- Create room
- Create barrels and racks
- Launch cannons
- Update ammos

# Blueprints
<img width="1614" alt="スクリーンショット 2023-11-25 11 36 58" src="https://github.com/jinyongnan810/UE5-learning/assets/29720903/033aac30-d1db-483c-bc8a-e2cb72ac23a9">


# Tips
## Copy objects
- Press option when dragging object automatically makes copies.
- Apply for multiple objects' copy

## Import assets
- When downloaded from marketplace, just add to the project.
- When downloaded a zip file.
  - Open `.uproject` file
  - Go to content drawer
  - Right click the folder, then migrate.
  - Select target project's content folder.

## Update to reliable collision
- Go to the object view.
- Delete current collision.
- Add 10DOP collision according to the shape.

## Extract blueprint logic as Function
- Select nodes and right click, collapse to function.
- If the function only for calculation(no side effects), check pure to omit execution arrows.

# Create room
## Making a room
- Open actor placement panel.
- Go to geometry.
- Add cubic(cube 1), set size.
- Copy the cubic(cube 2), increase the size by about 200.
- Make cube 1's brush type to be substract.
## Decorating the room
- Pull mesh on to walls.
## Make windows
- Also make cube with brush type of subsctract and fix it to the wall.

# Create barrels and racks
## Barrel
- Drag a barrel to the scene.
- Make it a blue print.
- Set physics.
## Racks
- To make two objects become one, drag the second object not to the scene, but under the StaticMeshComponent.

# Launch cannons
## Spawn
- Drag a Space Bar, then drag it to SpawnActor.

## Shoot at center of the camera
- Get player pawn.
- Get actor location and link it to SpawnActor location.
- Get control rotation and link t to SpawnActor rotation.
- Get Static Mesh Component, then get Forward Vector, multiply return value by 4000 and link to Add Impluse.

# Update ammos
## Store variable
- Window->My Blueprint->Variables->add

## Update ammos
- Drag variable to blue print to get or set itself.
- After Add Impluse, get ammos and substract it by 1, and set ammos.

## Check ammos
- When Space Bar pressed, check ammos is greater than 0 by drag to Branch.
- Link if true to SpawnActor.

# Reload level
- Get current level name.
- Open level by name.
