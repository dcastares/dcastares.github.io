Running the Profiler in Unity is a great way to understand what is happening in our game, but when a frame is not performing well, it’s not always obvious why. We have to capture the data, inspect the timeline, and dig through samples to find the culprit.

In day-to-day development, I often want a quick first pass to identify the biggest contributors, spot suspicious spikes or allocations, and decide what to investigate next. That’s where AI can help, by turning a captured frame into a short list of hypotheses to validate in the Profiler. It’s not a replacement for profiling, but it can speed up the initial triage and help you decide where to look first.

The only issue is that when we save Profiler data, we get a binary file that LLMs can’t read directly.

To solve this, I’m using this tool <a href="https://github.com/dcastares/unity-profiler-data-exporter" target="_blank">unity-profiler-data-exporter</a> (a fork from the tool from <a href="https://github.com/steve3003">Stefano Di Palma</a> I fixed to make it work with latest Unity versions) which lets you export a frame from the Profiler as a JSON file. With that, you can talk with your favorite LLM about what is happening in your game.

<h2>Workflow</h2>

Capture the problematic frame in the Unity Profiler.

Export that frame to JSON with unity-profiler-data-exporter.

Paste the JSON (or relevant parts) into your LLM along with a short question, for example: “What are the top contributors, and what should I check next?”

Validate the suggestions back in the Profiler and iterate.

What AI can help you spot quickly

Main thread bound frames vs render thread or GPU bound symptoms

GC allocations and spikes that hint at per-frame allocations

Expensive hotspots like Camera.Render, animation updates, physics steps, or Script.Update loops

Repeated calls or unusually deep stacks that point to a runaway system

Sudden spikes caused by asset loading, instantiation bursts, or expensive one-off work

<h2>Note on privacy</h2>

Profiler captures can contain project-specific details. If you’re working on proprietary code, consider sanitizing the data, removing identifiers, or using a local model before sharing it externally.

If you have comments, questions, or a way to improve it, shoot me an email!