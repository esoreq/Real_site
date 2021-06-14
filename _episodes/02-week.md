---
title: "Staying sane while converting a notebook to pdf"
author: "Dr. Eyal Soreq" 
start: true
date: "15/06/2021"
teaching: 60
exercises: 0
questions:
- Why export a notebook to pdf 
- How to export a notebook to pdf 
objectives:
- Learn how to create a reproducible report from a notebook

---
# Staying sane while converting a notebook to pdf

## Why export a notebook to pdf 

Often, a descriptive report is written by the researcher as part of a process, and there is no definitive audience, despite the researcher's capability to point to potential future directions at the beginning or end of the report. Since the main purpose of a descriptive report is to present an overview of the object of study, the report must convey all necessary information in an easy-to-understand form, not forgetting the reliability of the findings and the area of validity, which is common to the overall  population of the study. A reader should always be able to investigate the reliability of results, which means the report should contain all the pertinent data for this assessment, including the general sources of criticism, the type and distribution of data, and if applicable the significance level of preliminary tests. Descriptive reports cannot be assumed to immediately convey the true value of the study. Instead, it is entirely possible that the researcher is presenting to the public something it does not yet realize needs to be addressed. Therefore, you should create a report that captures the reader's attention and keeps it until the very end.

Reports tend to change a lot throughout different stages of a project, starting out minimal, but getting more and more comprehensive as the project ends and you have a more focused goal and problem to solve. In this sense, it makes sense to create an automatic report structure that can change  and adapt without much effort from the creator. 

# How to export a notebook to pdf 
- In order to create a PDF file from a notebook that contains some information, you can simply open the file menu and select export notebook as pdf
- However, this export cannot be considered a scientific report, as it lacks much of the structure and form expected from one.
- Fortunately, we can configure jupyter to produce polished reports with little effort, so we can produce reports at any point in the project cycle with one command

# Creating a reproducible notebook to pdf export  

- To create a reproducible pdf export, you need to generate a templete file that contains all the information needed to produce such a report. 
- We will be using a software called [nbconvert](https://nbconvert.readthedocs.io/en/latest/) to manage our conversion from jupyter to pdf, under the hood it uses a package that is called [Jinja](https://jinja.palletsprojects.com/en/3.0.x/) that converts that Jupyter notebook into a [LATEX](https://www.latex-project.org/) file 
- The latex file is then converted to pdf using another software called [pandoc](https://pandoc.org/)
- It is important to note that these templete files can become complex and I am just providing you with a simple working example here 
- To produce such a template file we will run the following cell 


```python
%%writefile 'my_pdf_template.tex.j2'
((*- extends 'latex/style_jupyter.tex.j2' -*))

((* block docclass *))
  \documentclass[12pt]{article}
((* endblock docclass *))

((* block packages *))
((( super() ))) % load all other packages
\usepackage{authblk}
((* endblock packages *))

((* block margins *))
\geometry{verbose,tmargin=1in,bmargin=1in,lmargin=0.75in,rmargin=0.75in}
((* endblock margins *))

((* block title -*))
((( super() ))) % load all other packages
\title{Composition of a Reproducible Descriptive Report}
((*- endblock title *))

((* block date *))
\date{\today}
((* endblock date *))
    
((* block author *))
\author[1]{Eyal Soreq+}
\author[2]{Also Eyal Soreq}
\affil[1]{UK Dementia Research Institute, Care Research \& Technology Center 929 Sir Michael Uren Research Hub, London}
\affil[2]{Department of Brain Sciences , Imperial College London}
((* endblock author *))

((* block maketitle *))
    \maketitle
    \tableofcontents
    \pagebreak
((* endblock maketitle *))
```

    Overwriting my_pdf_template.tex.j2


#### Let's unpack the structure 

1. `((*- extends 'latex/style_jupyter.tex.j2' -*))` tells the software to use an existing template that was written by the nbconvert team to parse the content of the notebook into the latex format 
1. `((* block <some word> *)) ... ((* endblock <some word> *))` creates a call that tells Jinja to find the contents of a block and replace it with your content 
1. ` \documentclass[12pt]{article}` defines the type of document you wish to create (see [Creating_a_document_in_LaTeX](https://www.overleaf.com/learn/latex/Creating_a_document_in_LaTeX))
1. Similar to Python, Latex has many packages created by users in the Latex community. Here for example we are loading [authblk](https://ctan.org/pkg/authblk?lang=en) to have more flexibility in author creation. Under the hood many other packages are loaded.
1. `((* block margins *))` are the way in which we can define the final report papaer margins
1. `\title{Composition of a Reproducible Descriptive Report}` is a pure latex command decalring the name of the title as a variable of the document
1. `((* block date *))` creates a variable of type data that updates it to today
1. `((* block author *))` deffines authors and affiliation
1. The `((* block maketitle *))` uses a Latex function to create a title page using the variables you defined previously using the `\maketitle` command
1. We also include table of contents using the command `\tableofcontents`
1. And we finish with a `\pagebreak` command to differentiate the rest of the report from this part  

## Using the template file 

The simplest way to use this template is by creating a configuration file that defines it and allows additional parameters to be defined, which we will not cover in this tutorial.


```python
%%capture
%%writefile 'cfg.py'

c = get_config()
c.NbConvertApp.export_format = 'pdf'
c.TemplateExporter.extra_template_basedirs = ['.']
c.Exporter.template_file = 'my_pdf_template.tex.j2'
```

We are creating a configuration file which can be used to control various processes that require specific variables. You can read more about how this works [here](https://ipython.org/ipython-doc/3/development/config.html).

# Bringing it all together

Before we can export anything we need some content to include in the report 
At the end of this course you are expected to produce a Reproducible Report containing some novel material produced by you representing your journy in the course. 


## Composition of a Basic Reproducible Report

Formally, a research report usually consists of the following parts:

1. Title page
1. Abstract
1. Table of contents
1. Introduction
1. Methods
1. Results
1. Discussion/Conclusion
1. Bibliography

## The Title Page

- Other then the the title this page contains
  - The name of the author or authors 
  - Their current affiliation
  - And, the date in which the report was generated
- Sometimes it will also include the table of contents   


## Abstract

The abstract of a report is usually a paragraph up to 300 words long summarizing the main points in the  following order:

1. The goal of your study and the research question(s) you examined
1. A description of the study's design
1. Major findings or trends that you discovered
1. A brief summary of your interpretations and conclusions


Then we use the display IPython function along with the Latex function to render a Latex box in the output. Additionally, I use a new formatting method that differs from the `f-strings` we used before. 
Here, we are just instructing Python not to process special characters, so the forward slash and  curly brackets are not processed, and we can write pure text that latex can interpret.


```python
display(Latex(r'''
\begin{abstract}
Insert ABSTRACT here according to subheadings and structure below;
general rules of thumb for abstract writing: 
should be 250-300 words long: 
use active voice but avoid “we did” or “we found”; 
numbers over 10 do not need spelling out at the start of sentences;
sentences starting with a number do not require a capital letter;
p-values should always be accompanied by supporting data
denominators should be given for percentages
abstracts do not need references 
\end{abstract}
'''))
```


~~~latex
\begin{abstract}
Insert ABSTRACT here according to subheadings and structure below;
general rules of thumb for abstract writing: 
should be 250-300 words long: 
use active voice but avoid “we did” or “we found”; 
numbers over 10 do not need spelling out at the start of sentences;
sentences starting with a number do not require a capital letter;
p-values should always be accompanied by supporting data
denominators should be given for percentages
abstracts do not need references 
\end{abstract}
~~~~


This method can be used to inject any latex box in theory. 

# Moving to the introduction  

Next, we will include some text using the Markdown heading structure we covered in the  bootcamp. This will usually be some expansion of the first sections of the abstract. 

Introductions take readers from general to specific. In it, we summarize what's known about the topic, set the scope, context, and importance of the research. A problem, accompanied by a hypothesis or a series of questions, explaining briefly how the method works, is the purpose of the work. You could also describe how your paper will be organized, and describe what your study might find out.

Exploratory research (sometimes called hypothesis generating) is about finding how variables influence each other. This approach means the researcher doesn't have any preconceived ideas or assumptions.  
A confirmatory study (also known as hypothesis testing) is one in which the researcher has a pretty clear idea about the relationship between variables. Here, the researcher is trying to find out if a theory, or hypotheses, is supported by data.  

The same data can be viewed from different angles, but as datasets become more complex (i.e. more factors are present), it is very challenging to conduct pure exploratory research and some expectations should exist about strong relationships previously described in the literature. 

Therefore, in the introduction, it is common to cite previous works in order to put your own questions and ideas in context. When you constantly have to change or adapt the way your referencing looks and feels, this can be a painful experience. Thanks to the framework I'm showing you, this whole process becomes transparent: you just have to add four lines to your template file and create an external file containing your references. 

## Adding the bibliography block
In our new template, we are providing explicit bibliographic referencing style in the text, as well as an end-of-report reference section.

The following code appends a `((* block bibliography *))` to our template file (notice we added the -a option to append to the file): 

The block contains `\bibliographystyle{unsrt}` where we declare the style of the bibliography, and `\bibliography{ref}` where we point the notebook to a reference file.



```python
%%capture
%%writefile -a 'my_pdf_template.tex.j2'

((* block bibliography *))
\bibliographystyle{unsrt}
\bibliography{ref}
((* endblock bibliography *))
```

## Next we need to create the reference file 
Citing references with BibTeX is easy. All citations and references are automatically formatted in a style of your choice, so you only have to type them once.
BibTeX references are stored in a simple, plain-text file with a `bib` suffix. 
If you want to know more check the Overleaf page  [Bibliography_management_with_bibtex](https://www.overleaf.com/learn/latex/Bibliography_management_with_bibtex).

You can find citations easily by using Pubmed, Google Scholar, or another reference search engine. You can just copy and paste to add any citation to your ref.bib file as I do in the next cell:


```python
%%capture
%%writefile 'ref.bib'

@article{rule2018ten,
  title={Ten simple rules for reproducible research in Jupyter notebooks},
  author={Rule, Adam and Birmingham, Amanda and Zuniga, Cristal and Altintas, Ilkay and Huang, Shih-Cheng and Knight, Rob and Moshiri, Niema and Nguyen, Mai H and Rosenthal, Sara Brin and P{\'e}rez, Fernando and others},
  journal={arXiv preprint arXiv:1810.08055},
  year={2018}
}
          
@online{literateprogramming,
    author    = "Donald Knuth",
    title     = "Knuth: Literate Programming",
    url       = "http://www.literateprogramming.com/index.html",
    keywords  = "latex,knuth"
}          
```

Including a citation in the text uses a simple format of calling \cite{rule2018ten} command  \cite{literateprogramming} 

# The Methods 

Research methods describe the steps taken to investigate a research problem, and the rationale for using specific procedures and techniques to identify, select, process, transform and analyze data to explain the problem, thereby allowing readers to critically evaluate a study's validity and reliability. 

Methodology sections of research papers answer two main questions: 
## How were the data collected or generated? 

Include a data overview that has the following information
- Where is the data from
- Sample size
- Group/condition of intrest
- A full description of the other covariates of intrest
- What metrics are you using and how were they extracted

## What kind of analysis was done?
Include a method section that has the following information
- What are the different methods used in this report
- Briefly explain what they do and why they will be suitable for you to answer your questions.
- Cite the method in citations to allow anyone who is unfamiliar with it to learn more about it. 
- If this method was used previously to answer a similar problem consider citing that paper as rationale of usage.

Write in the past tense and be direct and precise.


# The Results 

You present the results of your study in the results section based on the methods (or methods) you used to gather evidence to support  your questions or observations. 

Presented results must follow a  logical sequence without bias  or interpretation. 

It is possible to link your results to previous findings that put your results in context and potentially lead to the next section of results. 

This section should include both tables and figures as means of supporting your claims.

# The Discussion/Conclusion

Describe any new insights you've gained while studying the problem and explain how that relates to your findings in your conclusion. You'll always tie the discussion back to the introduction by talking about your research questions or hypotheses and the literature you read. The discussion doesn't just repeat the first part of your paper; it tells the reader how your study added to their understanding of the research problem from where you left off at the  end of your review of prior research.

You should include a limitation section in which you discuss limitations in the design, methodology, or interpretation of the results. It refers to any challenges arising from unanticipated challenges, limited data, computational resources, or any other issue that you feel should be raised that can limit the generalizability, application, or utility of the study findings. 

# Importing packages,constants and style
Reports containing data-driven analysis and visualization will include a code cell (usually the first cell) in which we import packages, define constants, and define figure styles.


```python
from datetime import datetime
CURRENT_TIME = datetime.now().strftime("%d-%m-%y_%H:%M")
AUTHOR = 'ES'


from IPython.display import display, Markdown,Latex,HTML
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
%load_ext autoreload
%autoreload 2
plt.style.use('bmh')
```

# At the end of the report include export statement 
The last cell should include a cell that generates the report, this allows you to change some parameters at the top and hopefully just run the notebook to produce the report. 



```python
%%capture
%%bash -s "$CURRENT_TIME" "$AUTHOR"
mkdir -p pdf 
jupyter nbconvert --no-input --output pdf/some_notebook_$1_$2.pdf --config cfg.py  some_notebook.ipynb
```

## Let's unpack 

1. First, we use the magic command `%%capture` to capture the bash output and ensure it is not included in the report 
1. Next, we use the magic command `%%bash` with the `-s` option to pass variables from the Python scope to bash
1. We create the *pdf* output folder using `mkdir -p pdf`
Then we call: 
  -`jupyter nbconvert` to call the pipeline for nbconvert
  - with nbconvert's `--no-input` option, which tells it to ignore the code cells in  the notebook
  - This allows me to explicitly specify where and under what name my report will appear
  - I provide the name `pdf/` to indicate the report should be saved in the pdf  folder
  - The output file is given the name `some_notebook_$1_$2.pdf`
    - where `$1` is the first  variable `CURRENT_TIME`
    - and `$2` is the `AUTHOR` variable
  - Then I use `--config cfg.py` to tell the program to use the  configuration file we previously created 
  - Lastly, I tell the program which notebook to convert


Our focus this week was on style, from next week we will shift to content, implicitly assuming that style is covered 
