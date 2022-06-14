## Clicking an object in 2d: Raycast vs OverlapPoint

I was integrating a 2D Unity game into a larger project, that was using Raycast to detect what object in the screen the user was clicking on, and the app had the option "Queries Start In Colliders" disabled (in Project Settings>Physics 2D). With this setting disabled colliders don't work, so following recomendations in the forums, I had to change the implementation to use Physics2D.OverlapPoint instead of Raycast.

<h2>What is the difference?</h2>

While Raycast will send a vector in a given direction and detect what colliders are on the way, OverlapPoint simply uses a point in the screen and checks if there is a collider that overlaps that point.

In terms of performance, even while in 2D may not be that expensive, the team at Unity recommends using the least ammount of raycasts as possible in their <a href="https://learn.unity.com/tutorial/physics-best-practices#5c7f8528edbc2a002053b5b4"> Physics Best Practices document</a>.

<h2>So, is it the same? </h2>

No, it is not. A raycast can be used for many things as you will not always be sending it from the screen to the plane, BUT if you want to specifically detect objects being under the mouse or tap position in the screen, I'm confident that with few tweaks you can change the implementation from one to another with no drawbacks.

<h2>The Code</h2>

So the code to detect our object on click that might be something like this:

```csharp
if (Input.GetMouseButtonDown(0))
{
    Vector2 touchPosition = Camera.main.ScreenToWorldPoint(Input.mousePosition);
    Collider2D collider = Physics2D.OverlapPoint(touchPosition);
    GameObject gameObjectClicked = collider.gameObject;
    //do what you need to do
}
```

If you have a comment, a question or a way to improve it, shoot me an email!
