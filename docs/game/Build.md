# Build of Multiple Frameworks
We successfully packed everything, including unity, python, tensorflow, electron into one executable. So we can distribute our application easily to playtesters.

## Main Components of Build
When we work on unity, unity helps to build everything inside unity. When working on an electron, we use electron-forge to build everything in the electron. 
However, our application uses both unity,electron and python. And there are no official tools to build them together.

- **Electron native build**: We use electron-forge to build resources managed by electrons. The main difference between normal electron build and ours is that there are many resources not managed by electrons, such as unity codes and python codes.
- **Unity executables** :
There are two unity executables. One is a GUI for playing the game, another is the record playback app. In an ideal situation, these 2 should be combined into one app. Since unity build is very small, build twice is acceptable in size.
- **Python build**:
We discussed how to build python into unity in previous blogs(Week6). We analyze pros and cons on different approaches. We still use “python interpreter + source codes” for the same reason
- **Database**
These are all static files. Just copy it into the right directory. 


## Challenges and Solutions
### Build Python Environment
Even we built our unity app by using “python interpreter + source codes” for the source codes. We also need to consider the python environment.   
#### Provide installer in electron app
We put a python installer into the build, and provide the GUI for user to install the  python and tensorflow. 
This didn’t work well when we tested on teammates' computers. One problem is there are many installation configurations, such as version, path,etc. Unknown problem will happen if users don’t configure it in right way. Another problem is that some teammates already have installed the python in computer, but with different version  and environment
#### Prebuilt python environment into electron app (Final choice) 
To make the python environment more stable and convenient, we preinstall the whole python environment, including interpreter and dependencies, into the final executable.
Even though the final build grew from 250MB into 1.6GB, the plan is much stable and under control.


### Build Cross Different Frameworks/Platforms 
Our project is an example of multiple frameworks and platforms. 
When we want to distribute our project by binaries, we consider two stages:

1. **Prebuild**:
First stage is to build all modules in their native platforms, as we discussed in Unity, electron, and python. In our case, our biggest challenge is to build python codes. 

2. **Combination and Communication**:
When we say combine the build, it's mainly about how to manage the paths, how to read files in the build files. Almost all frameworks(in our case, Unity and Electron) have their own way to get dynamica relative path during runtime, so this is doable.
As for the communication, because we use socket to do the inter-process communication. As long as we use the right port, the operating system will handle the rest.

### Develop Mode VS Runtime Mode
Most frameworks have a way separate codes in development and codes in build. We have the same situation, because the way we find codes in other platforms is different between develop mode and build runtime. 

Now we need to manually redirect the codes(latest developer codes or codes in last version’s build) during the development. This is very inconvenient and very easy to cause bugs. 

Our solution next step, is to automate the multi-platform build procedure, so that we manage the relationship between develop and build. 
Manual operation is the devil, we need to wipe this out of our build procedure!

