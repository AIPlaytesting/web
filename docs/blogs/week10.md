# Week 10 : Preparing For Playtesting

This week was all about bringing together our app so that it can be used for playtesting. There was a significant progress on this front with multiple different windows in the app being added. There was some minor progress on the AI front which bumped the win rate up to a stable ~82% and a peak of 88%. This brings us closer to our goal of 90%. However, experiments with the AI have slowed down because a lot of our efforts are not focused on completing the app for playtesting.

## AI Updates
There were three areas where the AI made progress this week. Let’s get into each one by one:

### Reward Function
In another update to the reward function, we decided to use a peculiar kind of reward function. Up until now, we were using a Monte-Carlo estimation of reward for a state action pair. This meant that we take the final reward of the trajectory at the final step, then go back one step at a time and assign a reward (discounted by the number of steps from itself to the final step) to each state-action in the trajectory.

This week, the peculiar thing that we did was to first calculate this reward for each state-action in the trajectory and then use this to create something similar to a temporal difference target. This is achieved by going up the trajectory starting at the current state and replacing the current state-actions’s reward by an addition of itself and the next state-action’s reward.

This seems like a weird thing to do but it did end up giving us a little bit of a better result than what we have received earlier.

### Reducing Model Complexity
As a part of the push we are making to go towards creating an application for designers to use, we want to reduce the time it takes to train an AI model. One of the ways this can be done is by modifying the hyperparameters. For one, we reduced the model complexity by reducing the number of layers and also reduced the number of neurons on each layer. Another thing was to reduce the batch size during training. Earlier the batch size was set to a much higher value than required (512). Reducing the batch size delivered the same approximate win rate. A potential benefit of this could be that we are avoiding overfitting.

### Integration with the App
The last important piece of progress this week was to complete the module that allows training by clicking a button on the app. You can also watch the progress of training as well as watch as the progress of the app improves. Currently, this is the only feature in place but we are working on creating test data using the generated model and then visualizing that data in the app.

## Build Across Multiple Frameworks
This week, we successfully packaged everything; unity, python, tensorflow and electron into one executable. This allows us now to distribute our application easily to playtesters.

### Main components of build
When we work on Unity, Unity itself helps to build the game in Unity. When working on electron, we use electron-forge to build everything in the electron. 

However, our application uses both unity, electron and python. Unfortunately, there are no official tools to build them together.

- Electron native build: 

We use electron-forge to build resources managed by electron. The main difference between normal electron build and ours is that there are many resources not managed by electron, such as unity code and python code.

- Unity executables :

There are two Unity executables. One is a GUI for playing the game, and the other is the record playback tool. In an ideal situation, these 2 should be combined into one app. Since unity builds are very small, two builds are acceptable in size.

- Python build:

We discussed how to build python into unity in a previous blog post ([Week 6](https://aiplaytesting.github.io/blogs/week6/)). We analyzed the pros and cons of different approaches. We yet again decided use “python interpreter + source code” for the same reason

- Database:

These are all static files. These need to be copied in the correct directory.

### Several tries in python build
In the past, we said we built our unity app using the approach “python interpreter + source code”. But we actually only did half of it, the source code. We didn’t consider the python interpreter, in other words, the python environment.   

Providing an installer in the electron app
We put a python installer into the build, and provide the GUI for user to install python and tensorflow. 

This didn’t work well when we tested on a teammate’s computers. One of the problems is that there are many installation configurations, such as version, path,etc. Unknown problems can happen if users don’t configure it in the right way. An additional problem is that some teammates already have installed the python in their computer, but with different version  and environment.

### Prebuilt python environment into electron app (Final choice) 
To make the python environment more stable and convenient, we preinstall the whole python environment, including interpreter and dependencies, into the final executable.

Even though the final build grew from 250MB to 1.6GB, the build is stable and under control. This is very important for us because our app is built across so many frameworks.

### Insights and Problems
#### BUILD CROSS DIFFERENT FRAMEWORKS/PLATFORMS 
Our project is an example of multiple frameworks and platforms. When we want to distribute our project by binaries, we consider two stages:

**Stage1: Prebuild**

First stage is to build all modules in their native platforms, as we discussed in Unity, electron, and python. In our case, our biggest challenge is to build all of the python code. 

**Stage2: Combination and Communication**

When we say combine the build, it’s mainly about how to manage the paths, how to read files in the build files. Almost all frameworks (in our case, Unity and Electron) have their own way to get dynamic relative path during runtime, so this is not a problem.

As for the communication, because we use socket to do the inter-process communication, as long as we use the right port, the operating system will handle the rest.

### Develop mode V.S. build runtime
Most frameworks have separate code for development and build. We have the same situation, because the way we find code in other platforms is different between develop mode and build runtime. 

Now we need to manually redirect the code (latest development code or code in last version’s build) during development. This is very inconvenient and can potentially cause a lot of bugs.

Our solution in the coming week, is to automate the multi-platform build procedure so that we manage the relationship between development and build. Manual operation is the devil, we need to wipe this out of our build procedure!

## Data Visualization

This week we learnt how to use d3.js to build interactive and professional data visualizations. We can use it to develop the different kinds of data visualization we discussed last week. The data we currently use (in the pictures below) is dummy data. However, in the next week, we will get real data from AI Playtesting.

![](/images/week10_vis1.png)

![](/images/week10_vis2.png)


All in all, this week saw some much needed progress on the app. We are excited to see how playtesters respond during the playtesting session on 10-11 Nov.