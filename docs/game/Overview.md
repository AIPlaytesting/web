# Overview
This section is about engineering. During the project, we explore how to integrate AI into the process of traditional game development. We met mang challenges and learned many experiences.  So we put the experiences we think can be applied to the general case into this section.

If someone asked “I want to develop a game using AI to playtest, how to do this?”, then this section is one part of the answer.

## AI as tool in game development
We treat AI as a tool for the development team. Compared to other tools, this is more complex. The biggest reason making our AI tools so different is that it needs access to gameplay logic. In other words, it requires gameplay programmers to provide formatted APIs to AI, which is challenging because gameplay keeps changing during the development process.

## Challenges
### One codes for all situations
In our project, we have a game for players, a game for AI, and a game for playtest. In read production, the game itself keeps changing, so we cannot maintain 3 versions of games. Instead, we have one single version that can be played in different situations.
### Generialization
Because we want designers to get quick feedback on his design, we aim to reduce the communication between designers, playtesters and programmers.
We need to make our AI and game generalized enough so that we can build a tool, like our demo, designer can use this tool design and get feedback.
