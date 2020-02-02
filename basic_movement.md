# Unity Basic Movement


## Create a  Game Object
## Add Rigidbody2D
## Add Sprite Renderer and drag in sprite.
## Create new Script and add it to Game Object
### In Script:

#### Set move speed

#### Get Horizontal input 

```c#
float deltaX = Input.GetAxis("Horizontal") * Time.deltaTime * moveSpeed
// multiply by Time to make framerate independent
// then by speed bc we want the change in position
float deltaY = Input.GetAxis("Vertical")* Time.deltaTime * moveSpeed
```

#### Get Camera X,Y bounds

```c#
private void SetUpMoveBoundaries()
{
Camera gameCamera = Camera.main;
xMin = gameCamera.ViewportToWorldPoint(new Vector3(0, 0, 0)).x + padding;
xMax = gameCamera.ViewportToWorldPoint(new Vector3(1, 0, 0)).x - padding;
yMin = gameCamera.ViewportToWorldPoint(new Vector3(0, 0, 0)).y + padding;
yMax = gameCamera.ViewportToWorldPoint(new Vector3(0, 1, 0)).y - padding;
}
```

Run this method in `Start()`.

#### Update position within bounds of Camera
```c#
// transform.position.x is the current x position of the GameObject
var newXPos = Mathf.Clamp(transform.position.x + deltaX, xMin, xMax);
var newYPos = Mathf.Clamp(transform.position.y + deltaY, yMin, yMax);
transform.position = new Vector2(newXPos, newYPos);
```

We need to run this in `Update()`.

Then press play and try it out. That should do it~
