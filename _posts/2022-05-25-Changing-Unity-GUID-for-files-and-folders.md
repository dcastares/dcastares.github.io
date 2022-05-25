## Changing GUID for files and folders in Unity

When you are integrating one project within another or moving scenes between projects, you cannot have the same GUID in two elements, so if you don't change it, Unity will do it for you.

What are GUIDs? 

In Unity, GUIDs are unique identifiers that are automatically assigned by the system to each file and folder. Those ids are written in each .meta file that Unity creates automatically for each file we add to our project.

Why you should care about GUIDs? 

Let's say you have scripts, sprites, prefabs, or any other Unity component that are beign used in entities in your scene, for example, you have a Game Object that is using an image asociated to the SpriteRenderer component, and a C# script in that same object. That object under the hood will look for the asset by GUID, so if you import that scene to another project, and Unity by any chance change the GUID because the original ones are in use, those references will be broken, or even worst, pointing to a different asset making it more complicated to identify.

Long story short, I was manually replacing GUIDs with Visual Studio Code in my project when I found this package from Jeff Jadulco that you can add to your project before the merge, and change all the GUIDs and references straight from the Unity's UI. 
Thank you Jeff!

You can get the package here: https://github.com/jeffjadulco/unity-guid-regenerator and it's well documented on how it works and how to use it.