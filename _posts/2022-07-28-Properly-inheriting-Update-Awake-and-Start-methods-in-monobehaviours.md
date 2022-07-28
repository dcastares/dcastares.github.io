## Warning "Use the new keyword if hiding was intended" in Unity's MonoBehaviour class

Talking with the team about this warning realized there is a lot of confussion among new Unity developers around how to properly inherit a class that inherits itself from MonoBehaviour and keep the Update, Start, Awake and other parent's methods working properly (OnEnabled, OnDisabled, LateUpdate, FixedUpdate and so on). When you just use autocomplete to create the methods, in the child class you get a warning saying "Use the new keyword if hiding was intended", as it assumes you are trying to hide the parent method, but is probably not what the developer is trying to achieve in most cases, so I decided to put a chunk of code here for guidance.

<h2>Code in the parent class</h2>

In the parent class, when you specify the original methods that you intend to extend in the child, you have to specify the keyword "virtual" in the declaration, this way the compiler will know it can be later on overriden in a derived class. 
So let's supouse we want Update() and Start() working in our child, the code would be something like this.

```csharp

    public class ParentClass : MonoBehaviour
    {
        protected virtual void Start()
        {
            //configuration stuff
        }
        protected virtual void Update()
        {
            //things to do every frame
        }
    }
```
That way when you write the methods in the child, the compiler will know you want it to override those.

<h2>Code in the child</h2>

In the child we will simply write the override keyword in the declaration to let the compiler know we want to do so, and if we want to run the code in the parent, just call the original method using base.Method(), or not if you just want to completely override it.

```csharp
public class ChildClass: ParentClass
{
    protected override void Start()
    {
        base.Start(); //you can run parent's code at any moment you need to
        //configuration stuff just in the child
    }
    protected override void Update()
    {
        base.Update();
        //things to do every frame just in the child
    }
}
```
Of course there are tons of scenarios where a different approach would be better used, but in my experience this work for most cases where you need to extend the MonoBehaviour functionality.

If you have a comment, a question or a way to improve it, shoot me an email!
