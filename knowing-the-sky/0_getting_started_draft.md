# Getting Started

This document is intended to teach you everything you'll need to know in 
order to use the interactive content in _Knowing the Sky_. It includes:

* how to download all the content from GitHub
* how to create Python environments
* how to run the Jupyter Server
* how to interact with a Jupyter Notebook
* basic technical background for alll these topics

If you already know how to do all this, you can skip this document.

## What is Jupyter Notebook?

Jupyter Notebook is an interactive coding environment. It can run
code in 
[many different languages](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels), 
and can also present formatted text and multimedia content. _Knowing the Sky_ 
uses it to let you run Python code. (We'll give more details about how that
works in a later section.)

It's important to know that even though you use Jupyter Notebook in a 
browser, that doesn't mean it has to connect to the Internet. Most people 
who use Jupyter Notebooks just run the Server "locally" (meaning on their 
own computers), because it's faster and you don't have to do complicated 
things with accounts and passwords to make it secure. If you follow the 
instructions in this document, you'll be running Jupyter on your own 
computer. This means that any changes you make to the Notebook files are 
totally private, you can back your changes up any way you want, and you 
won't even need a network connection to run them (although some of them 
contain specific sections of code to download data from the Internet).

One more small note: people often use the phrase "Jupyter Notebook" to 
refer to both the coding environment and to individual Notebook files, which
can be very confusing. We'll try to be careful about that and write "Jupyter 
Notebook file" when we're talking about a specific file instead of the 
environment.
 
## Technical Requirements

### Supported Hardware and Operating Systems

These instructions will let you install _Knowing the Sky_ on most laptops 
and desktops. You will need to be running Windows, MacOS, or Linux. (It's 
technically possible to set it up on a Chromebook, phone, or tablet, but it's
complicated and potentially buggy, so we don't support those platforms.)

Your computer should have at least 4 GB of RAM, 4 GB of free disk space, 
and a 64-bit CPU architecture. Most computers less than 10 years old will 
work fine.

You will need an Internet connection to do the initial installation and 
to run the parts of the content that download scientific data. There's no 
real-time networking involved, so the connection doesn't have to be 
fast, but if it's really slow or shaky, it might get frustrating. 

### Exceptions

If you're using a work or school computer that doesn't give you permission
to install software, these instructions won't work. You'll need to talk to
your system administrator to figure out how to set things up.

Similarly, if you're on a network that only allows access to a specific 
list of sites, you might need to talk to your systems administrator to get
permission to download the software and data.

## Installation

To run Python code in a Jupyter Notebook, you need to have Python and any 
extra "dependencies" (things the code needs that don't come included with 
Python) installed on your computer. You also, of course, need the actual
Jupyter Notebook file. This section contains step-by-step instructions for 
setting up your Python environment, downloading the _Knowing the Sky_ 
content, and running the Jupyter Server so that you can use the Notebooks.

### 1. Install Conda

We think the best way to set up Python for most open-source projects is to 
use the Conda package manager to download software from a 'channel' called
conda-forge. 

We prefer a version of Conda called Miniforge. It is provided by the conda-forge
community. 
[You can get the Miniforge installer from its GitHub page.](https://github.com/conda-forge/miniforge)
Just go to that page and follow the instructions in the 'Install' section.
During the installation process, just accept the defaults and say 'yes' to any 
prompts unless you have some other specific preference.

#### Tips

1. If you have an old version of Conda installed on your computer that you're
not using, you should probably uninstall it before you install Miniforge. The
rest of these installation instructions might not work correctly with different 
versions of Conda, and it's usually a bad idea to have multiple versions of
Conda installed on your computer.
2. Make sure you follow the version of the instructions for your operating system.
On MacOS, you should enter the command in the instructions in the Terminal 
program unless you have a different preferred console.
3. If you download the installer by clicking on a link rather than using a shell
command, make sure you pick the "Miniforge3" version of the installer, not "Miniforge-pypy3."  
Also make sure you pick the version that matches your operating system
[and CPU architecture](#what-kind-of-architecture-am-i-using).
4. If you have trouble, there are lots of tutorials on the Internet.

> INTERNAL DRAFT NOTES
> 1. Conda doesn't currently support Windows on Arm.
     However, they're planning to do this soon, and I expect they'll do it the
     time we ship, but we should keep an eye on it.
> 2. The console command on the page does the processor architecture thing
     automatically for Mac and Linux, but I'm not sure everyone will use it.
> 3. TODO: provide links to up-to-date tutorials closer to our ship date.

### 2. Get the _Knowing The Sky_ content

The rest of the _Knowing the Sky_ content lives in the same GitHub 'repository' 
as the document you're reading right now. GitHub is a popular platform for 
distributing and keeping track of changes to files. While you can browse GitHub on
the web, the most effective way to download code from GitHub is by using
the `git` application, which makes sure the code is well-organized on your computer
and lets you reliably keep it up to date. We'll do that by running shell commands 
to install `git` using `mamba` and then fetch the content with `git`.

#### Where to Run these Commands

On MacOS and Linux, `mamba` is fully compatible with built-in terminal programs. 
On MacOS, you can just use Terminal, and if you're on Linux, you probably already 
have a favorite console. On Windows, however, you can't use the built-in 
Command Prompt or Powershell programs. The Windows Miniforge installer also
installs a terminal program called 'Miniforge Prompt', which you can now
find in your Start Menu. You can use it to run these commands.

#### Install `git`

From the command line, run `mamba install -n base git`. This means "install 
the `git` package into the base conda environment" (we'll explain more about 
environments in a minute). Say yes to the prompts. Now you have `git`!

**TODO: link to more information on shell commands for the interested,
probably a sanitized version of our internal tutorial.**

#### Download _Knowing the Sky_

Navigate to wherever you'd like to download the _Knowing the Sky_ content
by using the `cd` command. For instance, if you'd like to download it to a 
subfolder of a folder in your home directory called 'projects', run `cd projects`.
If you want to download it into a subfolder right under your home directory, 
you can just stay where you are.

Then, download the content by running 
`git clone https://github.com/MillionConcepts/knowing-the-sky.git`.
This means: "make a folder and download all the files from the repository, 
into that folder, along with information about their modification history". 
Now, if you run `ls`, you should see a new folder named 
`knowing-the-sky`.

### Creating a Conda Environment

Conda helps Python dependencies stay well-organized by creating distinct "environments" 
and making sure that all the software in an environment is mutually compatible.
The `(base)` text you see in front of your prompt is a signal from Conda that
you're in the Conda environment named 'base', which is the default environment
created with every Conda installation.

It's generally a good practice to make a separate Conda environment for every 
Python project. _Knowing the Sky_ includes a Conda environment file -- a 
specification for a Conda environment that can run all its content. To 
create that environment, run `cd knowing-the-sky` to move into the repository
folder, then run `mamba env create -f environment.yml`. This means 'create a 
new Conda environment based on the specification in the environment.yml file.'
Say yes at any prompts and wait for `mamba` to download and organize the packages.

After `mamba` finishes, you can then activate the environment by running
`mamba activate knowing-the-sky`. When you run that command, the `(base)`
in front of your prompt will change to `(knowing-the-sky)`. When an environment
is active, shell commands you run will execute the versions of the software 
installed in that environment. **IMPORTANT:** you should always have the
`knowing-the-sky` environment active when you run the Jupyter Server
to use the `knowing-the-sky` Notebooks. It may not run, or run in expected 
ways, if you don't have `knowing-the-sky` active.

At this point, your installation is complete!

## Using Jupyter Notebook

> DRAFT NOTES:
> 1. I know it might be a Book or whatever, so the initial subsections here 
are provisional.

### Starting Jupyter Server

To use a Jupyter Notebook, you need to have Jupyter Server running. You can
run Jupyter Server from the command line by running `jupyter notebook`. 
This should open a browser window with the Jupyter Notebook interface. 
Remember to have the `knowing-the-sky` environment active.

### Opening a Jupyter Notebook File

In your browser, you should see the 'home page' of the Jupyter Notebook 
interface, which is basically a file manager. You should see all the files
in the base directory of the repository. If you click on the `knowing-the-sky` 
subfolder, you'll see a bunch of .ipynb Jupyter Notebook files. If you click
on a Notebook file, Jupyter will open it in an interactive session. 

You can now continue to the `0_getting_started_companion_notebook.ipynb` for 
a quick tutorial on how to use the Notebook interface.

### General Notes on Notebook

Most ways of executing code run that code 'non-interactively', meaning the
entire program runs all at once, stopping to check for input only if those
checks are specifically programmed into the code.

By contrast, Notebooks let you write and run little sections of a program at 
your own speed. If you've ever used an interactive session in any programming 
language, from the Python interpreter to the MATLAB command window, you're 
familiar with the basic idea. 

The biggest difference between traditional command-line interactive sessions 
and environments like Notebook is the concept of persistent cells. When you 
run a cell, all the code in a cell runs at once, just like when you run
code on a command line. However, that code persists as an editable cell in 
your window. You can immediately edit the code in a cell and run it again,
and more generally run cells in any order (no matter how they're organized 
on the page).
 
This gives you a great deal of flexibility. You can examine the output of 
individual steps before you continue to the next one, figure out what to 
write next, or decide to go back and change something. This makes Notebook 
very popular in applications ranging from data exploration to teaching to IT.
[This flexibility also has some downsides.](#downsides-of-jupyter-notebook)


## Appendices

### What Kind of Architecture Am I Using?

* MacOS: [Follow the instructions on this Apple Support page to find out whether you have an Apple Silicon Mac or an Intel Mac.](https://support.apple.com/en-us/HT211814)
  If you have an Apple Silicon Mac, install Miniforge3-MacOSX-arm64. If you have
  an Intel Mac, install Miniforge3-MacOSX-x86_64.
* Linux: Open a terminal and run `uname -a`. If it prints 'amd64' or 'x86_64',
  install Miniforge3-Linux-x86_64. If it prints 'aarch64' or 'arm64', install 
  Miniforge3-Linux-aarch64.
  
**TODO: Windows instructions, pending Conda Windows on Arm support**


### Downsides of Jupyter Notebook
 
We love Jupyter Notebooks, but they're not appropriate for every programming 
task. Here are some considerations to keep in mind if you want to use them
for other projects:

1. Because of their flexibility and nonlinearity, it's easy for code in 
Notebooks to become disorganized. This means that it's usually not a good idea 
to write big complex applications entirely in Notebooks. Many developers
like to prototype individual sections of a larger program in Notebook, and, 
as the code becomes more complete, split it out into a regular Python module.
Then, they might go back to Notebook, import the code from their module,
and continue prototyping.
2. Unless you wrap them in a function, all variables in a Notebook are in 
global scope. This can cause lots of collisions between names in different
parts of the program, leading to very confusing bugs -- for instance, a 
function defined early in the file could accidentally reference a variable 
defined later in the file that you didn't even think of as related to that
function.
3. Notebook's history features mean that references to the outputs of 
individual cells hang around in memory if you don't explicitly clear the history. 
It's common for this to lead to memory leaks.
4. The 'loop' that lets Notebook work interactively can interfere with some
other kinds of asynchronous or multithreaded code.
5. If you accidentally run code that outputs an enormous amount of text, 
a bunch of huge images, or something like that, it can cause Notebook to become very
slow or even freeze -- and it can become slow or even impossible to open that
Notebook file later if that output gets saved into the file.
 