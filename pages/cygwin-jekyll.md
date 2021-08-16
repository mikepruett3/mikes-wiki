# Jekyll on Windows With Cygwin

[nathanielstory.com](http://nathanielstory.com/2013/12/28/jekyll-on-windows-with-cygwin.html) · by Posted by Nathaniel Story

### Introduction
Jekyll is a static web site generator that can be used to create blogs similar to this one (which is, of course, Powered by Jekyll!) It is, however, a bit of a pain-in-the-ass to install under Windows. I was able to get it to run under Cygwin, a Unix-like environment that runs on top of modern Windows operating systems (in my case, Windows 7 Professional). The instructions below assume you already have Cygwin installed, and that you are comfortable using the command line.

### Installing Jekyll
Jekyll is installed as a Ruby gem. Installation is as simple as:

1. Run Cygwin’s ```setup.exe```
2. Install the package ruby
3. Once Ruby is installed, run the following command to install Jekyll:

```gem install jekyll```

### Installing Pygments
If you’re a programmer, you’re probably going to want to include code in your posts. If you include code in your posts, you’re probably going to want it to be syntax highlighted. You’re going to need [Pygments](http://pygments.org/).

#### Install Python
Pygments is a Python library. So, you’re going to need to install Python:

1. Run Cygwin’s ```setup.exe```
2. Install the package python: *Python language interpreter* (select the 2.x package, not python3!)

#### Install easy_install and Pygments
*easy_install* is part of the setuptools package. Once [setuptools](https://pypi.python.org/pypi/setuptools) and the easy_install utility are installed, installing Pygments will be trivial.

1. Run the following command to install _setuptools_ and associated utilities:

```curl 'https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py' | python```

2. This will create a temporary file in your current directory. You’ll probably want to delete it:

```rm setuptools-2.0.1.tar.gz```

3. Run the following command to install Pygments:

```easy_install Pygments```

### Additional steps

You may encounter the following two problems.

You may see an error like the following when Jekyll encounters a post containing a highlight tag:

```
Liquid Exception: No such file or directory
 - C:\Windows\system32\cmd.exe in _posts/2013-12-22-my-post.markdown
```

Set the COMSPEC environment variable like below to fix this. I suggest adding it to your ```.bashrc``` file:

```export COMSPEC=/cygdrive/c/Windows/System32/cmd.exe```

You may see also see this error:

```Generating... which: no python2 in (/usr/local/bin:/usr/bin:...```

To fix this, create a symbolic link like the following:

```ln -s /usr/bin/python /usr/local/bin/python2```

### Finally
You should now be all set up to create your blog/static-site with Jekyll. You’ll probably want to refer to the extensive documentation on the official website.