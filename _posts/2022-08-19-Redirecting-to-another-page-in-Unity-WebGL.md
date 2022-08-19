## Redirecting to a different page in Unity WebGL from C# scripts

When you are building a game, app, or experience using WebGL in Unity, there are chances that you may want to redirect the user to a different page, depending on the flow of your site.

When you are working to publish your app in other platforms than WebGL, or using old versions of Unity, you can just call <a href="https://docs.unity3d.com/ScriptReference/Application.OpenURL.html" target="_blank">Application.OpenUrl</a> and get there.

This changed lately, according to Unity's documentation: <i>WebGL: From version 2019.4.25f1, 2020.3.5f1, 2021.1.2f1, and 2021.2.0a11, Application.OpenURL opens url in a new browser tab. In previous versions, Application.OpenURL opens url in the same browser tab, which terminates the running Unity application.</i>

So from now on, Application.OpenUrl will open the url in a new tab, with an ugly warning from the browser saying a popup was blocked (but that is another story).

<h2>How to open a URL from WebGL in the same page?</h2>

So if you are between the 1% of the people who is actually looking to redirect the page to another location, this is a possible solution.

We will interact with the scripts in the browser to perform an old good javascript redirect. For that we will have to create a jslib file as is explained <a href="https://docs.unity3d.com/Manual/webgl-interactingwithbrowserscripting.html" target="_blank">in the documentation here.</a>

First, you will have to create a folder <b>Plugins</b> under your Assets folder, and there place a text file with the extension ".jslib". Then open this file and write the following code in it: 

```csharp
var RedirectPage = {
    openUrl: function(link)
    {
        window.location.href = UTF8ToString(link);
    }
};

mergeInto(LibraryManager.library, RedirectPage);
```

And then from your C# code you can use it like this:

```csharp
using System.Runtime.InteropServices;

public class ClickHandler : MonoBehaviour
{
    [SerializeField] string url;

    private void OnMouseDown()
    {
#if !UNITY_EDITOR
        openUrl(url);
#endif
    }

    [DllImport("__Internal")]
    private static extern void openUrl(string url);
}
```
And that's it, you can replace the OnMouseDown with any method you need and is ready to go. Hope it helps!

If you have a comment, a question or a way to improve it, shoot me an email!
