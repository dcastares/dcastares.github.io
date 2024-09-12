## Analizing Unity Profiler frames with AI

Running the profiler in Unity is a great way to understand what is happening in our game, but when we get a frame that is not performing well, it is not easy to understand why.
We have to open the profiler, get the data, and then we have to understand what is happening.
But sometimes, we can get a frame that we want to analyze, but we don't want to spend more than 30 seconds doing it, because we have other more important things to do.

So, wouldn't it be great if we could use AI to help us with this? 

The only issue here, is that when we save the profiler data, we get a binary file that LLMs don't understand that well.

To solve this, I'm using this tool <a href="https://github.com/steve3003/unity-profiler-data-exporter" target="_blank">unity-profiler-data-exporter</a> that let's you export a frame from the profiler as a JSON file, so you can have a talk with your favourite LLM about what is happening in your game.

If you have a comment, a question or a way to improve it, shoot me an email!
