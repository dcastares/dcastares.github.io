## Moving the camera with two finger touch in Unity

I needed to let the user navigate a map using two fingers and swipe in devices, so I wrote this class you can attach to your camera in any 2D game. Also works with the mouse's right button so you can test it out in the editor.

```csharp
using UnityEngine;

public class CameraControllerBuilder : CameraController
{
    [SerializeField] private float topEdge;
    [SerializeField] private float bottomEdge;
    [SerializeField] private float leftEdge;
    [SerializeField] private float rightEdge;

    private bool isDragging = false;
    private Vector3 startCameraPosition;
    private Vector3 startMousePosition;
    private Vector3 newMousePosition;
    new void Start()
    {
        base.Start();   
    }

    void Update()
    {
        if (Input.GetMouseButton(1) || (Input.touchCount == 2))
        {
            newMousePosition = Camera.main.ScreenToWorldPoint(Input.mousePosition);
            if (isDragging)
            {
                transform.position = startCameraPosition + startMousePosition - newMousePosition;
                if (transform.position.x < leftEdge || transform.position.x > rightEdge)
                    transform.position = new Vector3(startCameraPosition.x, transform.position.y, transform.position.z);
                if (transform.position.y < bottomEdge || transform.position.y > topEdge)
                    transform.position = new Vector3(transform.position.x, startCameraPosition.y, transform.position.z);
            }
            else
                isDragging = true;
            SavePositions();
        }
        else if(isDragging)
        {
            isDragging = false;
        }
    }

    private void SavePositions()
    {
        startCameraPosition = transform.position;
        startMousePosition = Camera.main.ScreenToWorldPoint(Input.mousePosition);
    }
}
```
