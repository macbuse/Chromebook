# Latex on Chromebook

For the last five years I've been using a MacBook Air 13" as my principal computing device. My children are changing schools and needed computers :

- 17 year old son going to college
- 14 year old daughter going to high school.

The son got a bursary of 500 euros which he wanted to spend on a computer. I found a MacBook on sale at 850 euros so that I had to add another 350. My MacBook has been a very good computer:

- good screen
- excellent keyboard
- good battery management
- OS X seems to (still) run pretty well.

For my daughter I did Amazon Prime days and bought her qn Asus c301 Chromebook:

- 4GB ram, 128 eMMC, similar form factor to MacBook
- good screen
- nice keyboard
- good battery life
- Chrome OS.

She liked it. Did all the set up herself, already had a Google account for her Android phone. Actually I found another model the Acer Chromebook 14 on sale and bought it for myself. Unfortunately my daughter found this alumnium MacBook lookalike more alluring and I ended up with the Asus.

This is the story of how I set it up for work.


## Chrome OS 

According to [Wikipedia](https://en.wikipedia.org/wiki/Chrome_OS):

*Chrome OS is an operating system designed by Google that is based on the Linux kernel and uses the Google Chrome web browser as its principal user interface. As a result, Chrome OS primarily supports web applications*

### Philosophy

Personally I'm quite happy with this i.e. accessing an application via a web interface rather than a window manager. I've been listening to music via a [SqueezeBox server](https://en.wikipedia.org/wiki/Squeezebox_(network_music_player) for a long time. For work I switched from writing  Python scripts in Komodo edit to writing in the browser using *JuPyteR* a couple of years ago. 

### The challenge of LaTeX

According to [latex-project.org](https://medium.com/@b23llc/experimenting-with-chromebook-data-science-in-the-cloud-2bd84a68b934):

*LaTeX is a high-quality typesetting system; it includes features designed for the production of technical and scientific documentation. LaTeX is the de facto standard for the communication and publication of scientific documents. *

Actually there are two parts to a document preparation system:
- the backend which will compile a file to a pdf
- the frontend which is a text editor and preview window.

LaTeX is heavily used in maths and physics - so the challenge
is to get a functional LaTex backend and frontend on a Chromebook. I spent a couple of days browsing the web looking at different solutions to doing LaTeX on a Chromebook for example:

- https://www.overleaf.com/
- https://www.sharelatex.com/

both of which are **online** resources and I like being able to do things **offline**. I also looked into some workarounds using Android apps and [termux](https://medium.com/@b23llc/experimenting-with-chromebook-data-science-in-the-cloud-2bd84a68b934) but it seemed technically difficult to get the backend and fronetend to work.


So we are going to: 

- install a traditional LaTeX backend using a package manager.
- install a frontend that runs over a local web server.

If you really want to do anything *advanced* then you have to set up developer mode. I also opted to go for a *beta build* of Chrome as opposed to the stock *stable build*.


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

There is an exciting  new product 
[JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) which is intended to be the next generation in preparation of scientific documents
[extension to edit and preview LaTex](https://github.com/jupyterlab/jupyterlab-latex).

Change directory to **$HOME** and  run JupyterLab from a terminal by doing 
*/usr/local/conda3/bin/jupyter lab* which gives a message like

*The Jupyter Notebook is running at:
http://localhost:8888/?token=7a5236631e6af925f6057152468b4900b284646e0f82b081*

and you should paste this url into another window on Chrome.
Now you have an **offline** file editor.

### Crew and TexLive

To install TexLive I installed **crew** which is yet another package manager.
I followed the instruction [here](https://github.com/skycocker/chromebrew)
and used **curl -Ls git.io/vddgY | bash** as **wget**.


To find the package is easy with 
**crew list available | egrep tex\* ** 
then **crew install texlive** does the heavy lifting.
I checked everything was working by typing **pdflatex**.

### JupyterLab LaTeX

This was the hardest part for me at least because I made a mistake and kept overwriting my PATH so that *bash* and *sh* were no longer available. There are only two steps but I spent 8 hours trying to see what I was doing wrong.

In the terminal:

1. ** pip install jupyterlab-latex** will install the extension but it has to be configured.
1. **jupyter labextension install @jupyterlab/latex**
this may take a long time as there is a ton of **node.js** 
stuff to download and build. On my Asus the build took  182.25s.
1. The extension defaults to running xelatex on the server qnd I changed this to pdflatex. 
Generate a config file for JuPyteR
via **jupyter notebook --generate-config** then edit **/home/chronos/user/.jupyter/jupyter_notebook_config.py**
and add 
**c.LatexConfig.latex_command = 'pdflatex'**

### LaTeXing

Restart JuPyteR Lab, download [sample.tex](https://github.com/jupyterlab/jupyterlab-latex/blob/master/sample.tex) and open it using the file browser in 
Jupyter Lab. 

Delete the graphic code:

'\begin{center}
  \includegraphics[width=0.65\textwidth]{images/jupyter_logo.png}
\end{center}'

as we have barebones LaTeX
and haven't downloaded **jupyter_logo.png**.

Finally do alt-click (on the Asus) to get a dialogue and select preview latex.


![alt text][logo.png]











 


























