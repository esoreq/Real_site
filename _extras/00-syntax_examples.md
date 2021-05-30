---
title: "syntax_examples"
start: true
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
All of this is based on the following [website](https://carpentries.github.io/curriculum-development/developing-content.html)

# Episode files
The majority of a lessons content is in its episode files. Episode files are stored in the _episodes/ folder within your lesson repo (or in _episodes_rmd/ for lessons written in R). Episode file names must start with a two-digit identifier number (e.g. 01) followed by a short descriptive name, separated by a dash (-). For example 02-loop.md, 03-lists.md. The numeric identifier is used to place your episode files in the correct sequence within the lesson. Episode files are written in Markdown (more on that in a moment) or RMarkdown.

# Episode headers
When your lesson repository is created, it will start out with one pre-made episode file (01-introduction.md). You can use this file as a template for creating each of your episode files, as it provides an example of how these files must be structured. The content of this pre-made episode file is shown above:

For each episode, you will need to create a copy of this file and:

1. Replace Introduction with the episode title (not the lesson title) in quotation marks. The episode title will appear on the episode page and in the schedule that appears on the lesson homepage.
1. Enter an estimated number of minutes for teaching the episode and an estimated number of minutes for learners to spend completing challenge problems (including class discussion of challenge solutions). These time estimates will likely be updated by Instructors as they get real-world data on how learners respond to the pacing of the episodes, but it is useful to have a starting point to benchmark from. The lesson template creates a schedule from these time estimates and places it on the lesson homepage.
1. Replace Key question (FIXME) with 1-3 motivating questions for the episode, each on a new line and in quotation marks. These motivating questions will appear in the schedule on the lesson homepage.
1. Replace First learning objective. (FIXME) with 3-7 learning objectives for the episode, each on a new line and in quotation marks. For information on writing useful learning objectives, see the Developing Content chapter.
1. Replace First key point. Brief Answer to questions. (FIXME) with 3-7 major take-aways from the episode. For information on how to distill an episode’s key points, see the Developing Content chapter. Key points for all episodes are shown together in the lesson’s reference page.


## Episode content

After the YAML header, your episode file will contain the content for that episode. This content will likely include:

- paragraphs of text
- lists
- tables
- images or figures
- code chunks
- special blockquotes, including exercises and solutions (described below)

This content will be written in Markdown, a light-weight markup language that makes it possible to create fancy HTML pages using only a few formating tricks. In this section, we’ll cover only the Markdown syntax that you will need in order to create the content types listed above. You can find more information about Markdown at https://commonmark.org/help/.


### Paragraphs of text - 

To create text paragraphs in Markdown, just type as you normally would! 
1. A few neat tricks:
    - surround text with a single pair of stars (*) to make text italic (*italic*)
    - use a double pair of stars to make text bold (**bold**)
    - create headers by starting a line of text with two hash signs (##) There are lots of other fancy things you can do, but this should get you started!

1. Lists - To create a numbered list in Markdown, do this:

~~~
1. A
1. numbered
1. list
~~~
{: .source}

Hint: You can use sequential numbers if you want, but it’s easier to update the list later if you use only 1s. Markdown will create the sequence for you.

To create an un-numbered list in Markdown, do this:
~~~
* An
* unnumbered
* list
~~~
{: .source}

## Tables - To insert a small table into your episode, do this:

| Category | Item | 
|--------- | ---- |
| Food     | Sandwich |
| Drink    | Tea | 
| Food     | Apple |


~~~
| Category | Item | 
|--------- | ---- |
| Food     | Sandwich |
| Drink    | Tea | 
| Food     | Apple |
~~~
{: .source}

## Images or figures

![](../fig/fig_one.svg)

~~~
![Figure Description](../fig/figure_file_name.svg)
~~~
{: .source}

## Code chunks 

Code chunks that learners should type out with the Instructor should use the {: .source} tag as shown above. Chunks that show expected output should use the {: .output} tag. Chunks that show an expected error message should use the {: .error} tag.

~~~
This is a genral source tag
~~~
{: .source}

~~~
This is a genral output tag
~~~
{: .output}


~~~
This is a genral error tag
~~~
{: .error}


# Special blockquotes - 
Exercises, solutions, helpful tips, and a few other types of special information are formatted as blockquotes within the episode file. Each blockquote has the same general structure, but ends with a different tag. The ending tag determines how the blockquote will appear on the lesson webpage. The general structure of a blockquote is:

~~~
> ## Title
>
> text
> text
> text
{: .callout}
~~~

Which looks like this 

> ## Title
>
> text
> text
> text
{: .callout}

# There are different blockquotes tags

- `{: .callout}` for sharing an aside or comment. Use sparingly.
- `{: .challenge}` for an exercise.
- `{: .discussion}` for a discussion question.
- `{: .solution}` for an exercise solution.


> ## callout
>
> text
> text
> text
{: .callout}

> ## challenge
>
> text
> text
> text
{: .challenge}

> ## discussion
>
> text
> text
> text
{: .discussion}

> ## solution
>
> text
> text
> text
{: .solution}


> ## keypoints test
>
> - text
> - text
> - text
{: .keypoints}

## Nested blockquote
Exercise solutions are nested within the blockquote for that exercise, as shown below:


> ## challenge
>
> This is the body of the challenge.
> > ## Solution 
> >
> > This is the body of the solution.
> {: .solution}
{: .challenge}

{% include links.md %}


<style>
table { margin-left: auto;margin-right: auto;width: 50%;}
td {font-size: 50px; text-align: center; }
</style>


|&#128528;|&#128528;|&#128528;|&#128528;|&#128528;|&#128528;|&#128528;|&#128528;|
|&#128528;|&#128528;|&#128528;|&#128521;|&#128521;|&#128528;|&#128528;|&#128528;|
|&#128528;|&#128528;|&#128528;|&#128521;|&#128521;|&#128528;|&#128528;|&#128528;|
|&#128528;|&#128528;|&#128528;|&#128521;|&#128521;|&#128528;|&#128528;|&#128528;|
|&#128528;|&#128528;|&#128528;|&#128528;|&#128528;|&#128528;|&#128528;|&#128528;|





[slides](../slides/index.html)
