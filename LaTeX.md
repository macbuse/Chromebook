# Latex on Chromebook

For the last five years I've been using a MacBook Air 13" as my principal computing device. My children are changing schools and needed computers :

- 17 year old son going to college
- 14 year old daughter going to high school.

The son got a bursary of 500 euros which he wanted to spend on a computer. I found a MacBook on sale at 850 euros so that I had to add another 350. This is because my MacBook has been a very good computer:

- good screen
- excellent keyboard
- good battery management
- OS X seems to (still) run pretty well.

For my daughter I did Amazon Prime days and bought her an Asus c301 Chromebook for 240 euros:

- 4GB ram, 128 eMMC, similar form factor to MacBook
- good screen
- nice keyboard
- good battery life
- Chrome OS.

She liked it, did all the set up herself ( easy since she already had a Google account for her Android phone) but the ASUS is a bit plasticy. Hey for 240euros? Actually a couple of days later I found another model, the ACER Chromebook 14, on sale at the same price and bought it for myself. Unfortunately, my daughter found the Acer, which is a sleekish alumnium MacBook lookalike, more alluring and I ended up with the ASUS.

This is the story of how I set the ASUS up for work and, as a professional mathematician, this entails:

- setting up an environment for programming in Python (and other stuff)
- installing a document preparation system i.e. LaTex.

Curiously, it is **much, much** easier to do the latter if one knows how to do the former. I believe this is a question of imagination and understanding how modern technologies should fit together. In fact, the web seemed to be full of people searching a solution but *not seeing* that the solution to both these problems was almost the same. It took less than two days to have a fully functional environment. The key insight is to understand that Chrome OS is engineered to *support web applications* and that the *JuPyteR* project is a flexible web based development environment. 


Incidentally this document was prepared as in MarkDown using JuPyteR.

---

#### Who is this for

Most people who have a minimum experience of a Linux terminal and:
- know how to navigate in a **bash** shell 
- aren't frightened of **sudo**
- know where Linux should put stuff by default
- know what a package manager is (e.g. apt)
- are prepared to edit config files by hand.

---

## Chrome OS 

According to [Wikipedia](https://en.wikipedia.org/wiki/Chrome_OS):

*Chrome OS is an operating system designed by Google that is based on the Linux kernel and uses the Google Chrome web browser as its principal user interface. As a result, Chrome OS primarily supports web applications*.

### Philosophy

Personally I'm quite happy with this i.e. accessing an application via a web interface rather than a window manager. I've been listening to music via a [SqueezeBox server](https://en.wikipedia.org/wiki/Squeezebox_(network_music_player) for a long time. A couple of years ago, I switched from writing  Python scripts in Komodo Edit/Idle to using *JuPyteR* the browser. There are, undoubtedly, certain disadvantages to this method of development but these are outweighed by the advantages when, for example, exploring data.

### The challenge of LaTeX

According to [latex-project.org](https://medium.com/@b23llc/experimenting-with-chromebook-data-science-in-the-cloud-2bd84a68b934):

*LaTeX is a high-quality typesetting system; it includes features designed for the production of technical and scientific documentation. LaTeX is the de facto standard for the communication and publication of scientific documents. *

Actually there are two parts to a document preparation system:
- the backend which will compile a .tex file to a .pdf.
- the frontend which is a text editor and preview window.

LaTeX is heavily used in maths and physics. If one cannot build a functional LaTeX sytem on a platform then, as far as my colleagues are concerned, it is not a viable alternative to a MacBook say. So the challenge is to get both of these functioning  on the Asus Chromebook. 

### Existing solutions

I spent a couple of days browsing the web looking at different solutions to doing LaTeX on a Chromebook, finding  for example:

- https://www.overleaf.com/
- https://www.sharelatex.com/

both of which are **online** resources and I like being able to do things **offline**. I also looked into some work arounds using Android apps and [termux](https://medium.com/@b23llc/experimenting-with-chromebook-data-science-in-the-cloud-2bd84a68b934) but it seemed technically difficult to get the backend and frontend to work. Android apps appear, at least to me,  to run  in isolated environments and getting applications in different environments to talk to each other appears, at least to me,  impracticable.

----

## My solution

So what I am going to explain is how to: 

- install a traditional LaTeX backend using a package manager (crew).
- install a frontend that runs over a local web server (JuPyter lab).

Of course once the backend installed one can use vi(m) to prepare .tex files and scripts to compile and preview. But that's not an IDE...

This is all (a posterio) very easy to accomplish but it involves accepting the browser as a replacement for a traditional window manager as an app API. There are 5 easy steps, explained below, to getting everything up and going:

1. developer mode
1. terminal in Chrome OS
1. Anaconda - Python3 & JuPyteR
1. homecrew -- homebrew for Chrome
1. pip and jupyterlab-latex

---

### Developer mode, beta build 

If you really want to do anything *advanced* then you have to set up developer mode. I also opted to go for a *beta build* of Chrome as opposed to the stock *stable build*.

I went to the beta build (though it might not be necessary) because:
- I wanted to use Android apps like termux
- (maybe) get containers f or Linux apps like Inkscape but these are still in alpha.

Developer mode is **necessary**: 
it's really easy [here](https://medium.com/@dihuta/turn-on-developer-mode-on-chromebook-bd8a05c31bf9)



### The terminal

To get started in the Chrome browser type
ctr-alt-t to get a **crosh** terminal in q new tab and typing **shell** 
gets you a genuine **bash** shell for the user **chronos@localhost**.

After doing this I wanted to install **Python** and I found a guide on
[this site](https://wsvincent.com/install-python3-chromebook/).
There is the usual scary stuff, in particular installing to /usr/local
so you do a  **sudo chmod 777 /usr/local** before starting. After this it's not particularly difficult from the CLI

- download a binary to /Downloads/
- cd to /Downloads/ and do   bash Anaconda3*
- at the prompt change the installation directory to /usr/local/conda3
- add /usr/local/conda3/bin to your PATH

### Jupyter 

Actually you are installing **Anaconda** which comes with 
lots of other stuff in particular **Jupyter**. According to the 
[website](http://jupyter.org/)

*Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and narrative text.*

There is an exciting  new product called
[JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) which is intended to be the next generation in preparation of scientific documents and has an
[extension to edit and preview LaTex](https://github.com/jupyterlab/jupyterlab-latex).

Since it comes with **Anaconda** all you have to do to get this running  is to change directory to **$HOME** and,  in the  terminal, type 
**/usr/local/conda3/bin/jupyter lab** which gives a message like:

**
The Jupyter Notebook is running at:
http://localhost:8888/?token=7a5236631e6af925f6057152468b4900b284646e0f82b081
**

Now copy/paste this url into another window on Chrome to connect to the server so you have an  operational **offline** file editor (and much , much more).

### Crew and TexLive

To install TexLive I installed **crew** which is (yet another) package manager; following the instruction [here](https://github.com/skycocker/chromebrew) :

- to install I used **curl -Ls git.io/vddgY | bash** as **wget** failed.
- finding the package is easy with  
**crew list available | egrep tex\* ** 
- **crew install texlive** does the heavy lifting for TexLive.  There are messages telling you to install other TexLive packages using **tlmgr** as this is a minimal installation.

I checked everything was working by typing **pdflatex** in the terminal  but this is optional.

### JupyterLab LaTeX

This was the hardest part for me at least because I made a mistake and kept overwriting my PATH so that *bash* and *sh* were no longer available. There are only three steps but I spent 8 hours trying to see what I was doing wrong.

In the terminal:

1. ** pip install jupyterlab-latex** will install the extension but it has to be configured.
1. **jupyter labextension install @jupyterlab/latex**
this may take a long time as there is a ton of **node.js** 
stuff to download and build. On my Asus the build took  182.25s.

There is a third step that is not obvious: The extension defaults to running xelatex on the server and I changed this to pdflatex. 
- Generate a config file for JuPyteR
via **jupyter notebook --generate-config** 
- edit **/home/chronos/user/.jupyter/jupyter_notebook_config.py**
and add  **c.LatexConfig.latex_command = 'pdflatex'**

---

### Previewing a LaTeX document

Restart JuPyteR Lab:

- download [sample.tex](https://github.com/jupyterlab/jupyterlab-latex/blob/master/sample.tex) in the browser
- open it using the file browser in 
Jupyter Lab. 
- delete the graphic code:
'\begin{center}
  \includegraphics[width=0.65\textwidth]{images/jupyter_logo.png}
\end{center}'
this is necessary as we have barebones LaTeX
and haven't downloaded **jupyter_logo.png**.

Finally do alt-click (on the Asus) to get a dialogue and select preview latex. Voila:


![alt text][https://github.com/macbuse/Chromebook/blob/master/logo.png]











 


























