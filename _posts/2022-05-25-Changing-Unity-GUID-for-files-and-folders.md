## Changing GUID for files and folders in Unity

When you are integrating one project within another or moving scenes between projects, you cannot have the same GUID in two elements, so if you don't change it, Unity will do it for you.

<h2>What are GUIDs?</h2>

In Unity, GUIDs are unique identifiers that are automatically assigned by the system to each file and folder. Those ids are written in each .meta file that Unity creates automatically for each file we add to our project.

<h2>Why you should care about GUIDs? </h2>

Let's say you have scripts, sprites, prefabs, or any other Unity component that are beign used in entities in your scene, for example, you have a Game Object that is using an image asociated to the SpriteRenderer component, and a C# script in that same object. That object under the hood will look for the asset by GUID, so if you import that scene to another project, and Unity by any chance change the GUID because the original ones are in use, those references will be broken, or even worst, pointing to a different asset making it more complicated to identify.

<h2>So, what can I do about it?</h2>

Long story short, I was manually replacing GUIDs with Visual Studio Code in my project when I found this package from <a href="https://jeffjadulco.com/" target="_blank">Jeff Jadulco</a> that you can add to your project before the merge, and change all the GUIDs and references straight from the Unity's UI. 

You can add the package from the following git url in the package manager:

https://github.com/jeffjadulco/unity-guid-regenerator.git

After that, right click in your project files and just select "Regenerate GUIDS".

Thank you Jeff!

<a target="_blank" href="https://github.com/jeffjadulco/unity-guid-regenerator">You can get the package here</a> and it's well documented on how it works and how to use it.

If you have a comment, a question or a way to improve it, shoot me an email!