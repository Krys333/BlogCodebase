---
title: "Cursor and AI-Powered Agents - The AI TAKEOVER"
date: 2025-07-14
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["AI", "2025", "Cursor", "highlight"]
description: "I used Cursor for the past couple of months. My thoughts on current state of AI code agents."
thumbnail: "images/AI_Agents.png"
image: "/images/AI_Agents.png"
---

There is a ton of talk about AI right now. From the conception of ChatGPT, to image generation, to "We are all going to be replaced!". I will be honest. I have been spooked by the speed with which the AI tech has been advancing. 

Example - I used to dabble in graphic design, and let me tell you. While the industry has not been entirely replaced by AI, a big portion of it has sank overnight. Specifically SMEs looking for basic graphic design work, or ideas. Same goes to the copywriting industry. The best of the best have not been replaced> However, overnight AI has made us ALL at least average at writing and illustrating.

## Does the generation work for code? - the positives

I used Cursor for a couple of months now. Anyone that gave it a fair shake should be honest. It is a fantastic tool. I remember when I first fired it off. I loaded the repository and asked Cursor a question about the codebase. Promptly it started interpreting the code and searching the web for additional context. The agent swiftly followed up by inserting code directly into the open files as it produced an overview of the changes it made. 

Magic. It is scary how quickly an AI agent can introspect a complex codebase with surprisingly little direction. The ease of use and the degree with which it is integrated with the IDE are also breathtaking. The output - also impressive. Especially at first glance it looked like the solutions were precisely prescribed and executed. 

## In prolonged use, cracks appear

So Cursor can be great. Especially at small scale projects. If you ask it to write a script doing X for you, I have no doubt the output will do pretty much what it was asked. Where I have noticed the first problems, was when Cursor is used in a large-scale, complex codebases. If you ask the agent to build on what is already there, it is fast to suggest a myriad of ideas. Those tend to look great at first, but as I looked closer I noticed bloat and logic that should not have been there.

Example - Pretty please. Help me produce a mapping functionality letting me write Snowflake database types into parquet. Disclaimer, my prompt was A LOT more detailed.

The output looked convincing at first. The agent produced a series of mappings that I could insert into a SQL query to export my data. The changes were accompanied with ideas for mapping the data types and constructing the SQL query within Python.

This is when it hit me. The longer I looked at the code the more problems I have discovered. 

1) Many of the data types Cursor has dreamed up included types that are not seen or handled by Snowflake. 
2) The query construction was bloated and included A LOT of unnecessary options and functionality that have never been requested. Only serving to distract from the key functionality.
3) The outputs try to mimic the style of the codebase, but the patterns are often weirdly and poorly executed. 

Having took in all that was going on, I went about just rewriting the code myself anyway.
Having tried the agent on a range of other tasks and questions I noticed other patterns emerge.

- IT LIES (SOMETIMES).
  - This can happen even with very basic questions.
  - The Ai agent will be super confident when it hands you a hammer but calls it a screwdriver.
- Even when asked for a simple change, the agent often JUMPS at creating HUGE changes.
   - This makes me wonder whether it is configured to do this. Why not JUST STOP at a simple change? Be iterative. Work with the developer.


## Conclusions
As mentioned in the beggining, I do not want to be overly critical of these tools. They are achieving some amazing feats with how they are integrated with or IDEs and how promptly they can output various qualities of code. But as a summary here are some conclusions on the present state of the AI coding agents.

### Will AI take our jobs?!

This is a cool one because even if AI gets A LOT better at writing code (and we could somehow no longer police it's quality), it will still need capable developers to tape and implement everything in it's right place. These devs will need to know how the vast majority of underlying code works. They will need to know how it plays with other systems and how to integrate it. Or at the very least, know exactly what they need to ask for to get what they actually need. The result seems to be a continued need for highly knowledgable professionals.

### Is the technology good now?

Right now this point boils down to how you use these new tools. To maximise effectiveness, you will need to make your prompt as detailed as possible. You need to know what you need and more or less how you want it implemented. This means no "free lunch" for those completely in the dark about the technology or the system they are building. Best case scenario so far is that the AI agent will speed you up considerably. Most positive outcomes is having AI relieve you of having to write a ton of boilerplate code. 

### Will AI agent stunt growth of your average dev?

In short, yes. It's VERY tempting to take the path of least resistance. I can't describe how easy it could be to start generating garbage code that just about works, but is exponentially harder and harder to maintain. If we outsource our thinking, ultimately we will suffer. 

If used correctly however, it can bring about good things for learning as well. For example, I found having a prompt window right in my IDE very convenient for fast search of technical info. Another very useful use is prompting cursor to suggest improvements or spot inconsistencies. Sometimes the AI agent will come up with some great finds.

### The future

As it always was, make sure you try out "the new shiny" and sure you stay ahead of the game. I mean it. I feel like AI is here to stay as even in the current state it offers value. How this will shape the industry is a much more difficult question. Developers are unlikely to be removed and will instead need to adapt into more architectual roles (I suppose). What I find hard to imagine is how we will continue to develop our understanding of underlying technologies, while being pushed to move faster with AI churning out the code for us. Already we are cutting out juniors. The senior devs won't stick around forever either. So in a decade or so I imagine we will either, churn out generic code slop that few people understand. Or, we will hit another period of developer shortages and realise we needed junior devs all along. 
