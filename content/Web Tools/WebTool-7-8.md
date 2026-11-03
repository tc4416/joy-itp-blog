---
title: "WebTool: Week7+8 Midterm"
draft: false
---
#### Original Proposal
[Slides](https://docs.google.com/presentation/d/13tICUG-MVbqeXQ6b_CH2A1pcNVzRpwCk3Xtme-btLLs/edit?usp=sharing)
For the midterm, I wanted to make a tool that can help me with my project documentation. I personally struggle a lot to put together good documentation for my projects. Sometimes, when I get into the working stage, I can’t keep up with recording everything and writing down all the references I use. So I wanted to make this tool that aims to solve this problem.

Originally, I was thinking of having an HTML form response type of interface that can guide the user through entering important information and progress about their project. I was inspired by a web art piece, [whenwe.love/form](https://whenwe.love/forms/)by Chia Amisola. I liked the minimalist style, and thought that having a form with different types of questions could make the documenting process less painful. However, after thinking more about it and going through another cycle of documenting my projects for my midterms in other classes, I think simply having a fun interface would not solve the issue. It still requires me to dedicate time and a full window page to log my progress.

How I currently blog my projects is that I have multiple windows open on my desktop. I keep each window at a smaller size, stacked loosely, so that it is easier to switch between windows and tabs. I use the Obsidian editor and usually write my process in bullet points or short sentences. I also screenshot a lot and usually just paste my screenshots into Obsidian directly with cmd+v. Usually my initial entry comes out super messy, with lots of typos, sentences that have flow issues, repetitive words, and weird sentence structure. Sometimes I leave it as is if I don’t think anyone else will read the post. If it is for a bigger/important project or a required blog post for class, I read through what I wrote a few times and clean up the typos or weird grammar. And because I am not super confident with my writing, I use AI agents (Claude or ChatGPT) and prompt them to check the grammar and typos without adding/removing information or changing my writing tone and style.

<div align = "center">
<figure>
<img src="/media/webtool/midterm-screenshot.png" > 
<figcaption>An example mess of how my desktop would look like in the middle of working session</figcaption> 
</figure>
</div>

So I pivoted a little bit on the interface and the functionality of my blogging tool. I want it to be:
- Still usable when it is occupying minimal space on the screen. I use split view a lot on my laptop, so sometimes my blogging area gets squeezed into a thin section on the right side of my screen.
- Ideally, this tool should be like a floating sticky note that occupies a very small space. I found a Mac app called [drafts](https://getdrafts.com/) hat works very much the way I would want my tool to behave. It works like a Post-it and stays there when you switch screens. You can also call it from the top bar of your desktop.![[draft.mov]]
- Because I don’t have much experience making an app or a Chrome extension, I decided to start with a website. I want the interface to be vertical, where you can log entries line by line. One interaction reference that I thought of while doing this is the [Mist](https://www.getmistapp.com/) app.
<div align = "center">
<figure>
<img src="/media/webtool/midterm1.png" > 
<figcaption>Split Screen</figcaption> 
</figure>
</div>

#### The Tool
[Final Website](https://tc4416.github.io/web-tool-fa26/midterm/)
I made a bullet point style interface. When users are ready to put what they wrote into their blog editor, they can click submit and have the LLM API fix the grammar and output text (bullet points or paragraphs) that is ready to copy and paste.
#### Feedback
- I had my input styled as bullet points. It is how I usually blog things, but possibly not the case for most people. So I want to add a paragraph style input as well.
- The radio button is supposed to be for the output style. Bullet point output just fixes the grammar of the bullet point input, and paragraph style output constructs paragraphs with the information from the bullet point input. But during user testing, I realized that it is a bit confusing for people. They thought the option was for the input style, so I should fix that.
- So basically, options for input style and options for output style
- Need to figure out how to deal with the API key
- There is a bug where, when there is only one bullet point entry and the output style is set to paragraph, the LLM mistakes the bullet point entry for the prompt itself.
    - For example, if there is just one bullet point note saying “I need to look into xxx,” the AI model will return something like “Here are the resources you can look into about xxx.” This shouldn’t be hard to fix, though.
- Add a function that allows pasting screenshots
#### User Testing
![[webtool.mov]]![[webtool2.mov]]
#### AI Agent
I got a lot of help from AI agents for this assignment because of the time constraint I had (which was totally my fault haha). The following is a snippet of the Claude Code prompt history. The parts highlighted in red were my prompts. I was jumping between Claude in the web browser and Claude Code in VS Code, and unfortunately I couldn’t retrieve part of the conversation. For this assignment, I set up the initial HTML, CSS, and JavaScript, and coded the very simple layout by myself at the beginning. I figured out the text area setup and the basic array setup to log the input. I got the most help from AI on 1) setting up the project tabs + rendering the logged info when switching between tabs, 2) styling the website, and 3) setting up the API (I provided the class demo and told it to use only what I’ve learned).
![[Webtool Midterm Claude Convo.pdf]]