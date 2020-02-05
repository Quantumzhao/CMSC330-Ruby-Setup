# Overview: Ruby with VS Code

This is a tutorial on how to set up a *Ruby* development environment on *VS Code*

> Well, I think I don't really need to introduce VS Code, it is so well known ...

This tutorial includes: 

- [Basic *Ruby* language support](# Basic Installations), including:
    - Syntax highlighting
    - Basic auto completion and suggestions
    - *Git* managements
- [Advanced *Ruby* language support](# Advanced *Ruby* Language Support), including:
    - Lint (VS Code call this, *IntelliSense*) and suggestions given based on type system
    - Class hierarchy view
    - Inline documentation
- **Debugging** using a graphic user interface 

## Recipe

- Visual Studio Code
- A local machine
- Operating system includes and restricted to:
    - *Windows 10* (with *WSL* installed)
    - *Mac OS*
    - Linux

## Requirements

- Internet connection
- Have all necessary modules installed (i.e., have completed project 0)

Personally, I am using *WSL* on *Windows* with the distribution of *Ubuntu*. 

For Linux, (*Ubuntu* distribution), the steps should be reasonably the same (but of course Linux users don't need to setup *WSL* connection)

Things might be different on *Mac OS*, but basically the same. 

## Disclaimer

I am new to *Ruby*. To be honest, I don't have a complete knowledge of what the following steps are doing. These are solutions collected and organized from websites like *Stackoverflow* or something else. 

I cannot make sure that these solutions would work on your computer. If so, well, good luck then. 

If you manage to set up the configurations, I am not supposed to take any responsibility of the consequences. 

> I mean, they should work fine, but just in case. 

# Basic Installations

Linux (*Ubuntu*) and *Mac OS* users can directly jump to the [more important part](# 3. Install *Ruby* extension)

## 1. Set up connection to *WSL*

> Although I believe most of you should have done this step, but just in case. 

Go to *Extensions*, search **Remote - WSL**, it looks as shown:

<img src="image/rm_wsl_ext.png" alt="rm_wsl_ext" style="zoom:50%;" />

And download it. 

There should be a little "~>~^<^" like icon at the lower left corner like this:

![wsl_unactive](image/wsl_unactive.png)

## 2. Connect to *WSL*

1. Click this icon, and select **Remote WSL: New window** (or any other options if you like)

2. After doing this, *VS Code* will start to set up a connection. 

3. When we see this

    ![wsl_active](wsl_active.png)

    We are done. 

## 3. Install *Ruby* extension

Before move on to anything further, let's set up a test project to see if the following can work. 

> The following steps are so trivial that most of us should just ignore it. But it is here, just in case. 

1. Click the *Terminal* button on the menu bar and choose *New Terminal*
2. Create a folder
3. Open this folder

### The Actual Stuff

Go to *Extensions*, and search **Ruby**

<img src="image/ruby_extension.png" alt="ruby_extension" style="zoom:50%;" />

>  Actually this extension should be marked with a little star, meaning that it is a recommended extension

Make sure you install it on *WSL* (for *WSL* users)

It should also download some other dependent extensions, including:

<img src="another_ext.png" alt="another_ext" style="zoom:50%;" />

> There might be a little line of text saying that *Extension ... is disabled ...* I don't know what it exactly means, but just ignore it. 

## 4. Now try it

Open the project folder, and start editing. 

We can find some simple suggestions as shown: 

<img src="image/ruby_ext_default.png" alt="image-20200204132252676" style="zoom:50%;" />

The default suggestions can provide a fairly good amount of information, but they are only based on string literals. 

**Can we have better experience? **

Well, the basic *Ruby* setup tutorial has just finished. 

---

# Advanced *Ruby* Language Support

## Set up *IntelliSense*

In order to utilize the powerful functionality of *IntelliSense*, we need to install another extension, called ***Solargraph***, which can also be found on VS Code extension market. 

It looks like this:

<img src="image/sg_icon.png" alt="sg_icon" style="zoom:50%;" />

In addition to this, *Solargraph* also provides some very cool utilities such as:

- Inline documentation

    <img src="image/solargraph_usage_example.png" alt="solargraph_usage_example" style="zoom:50%;" />

- Hierarchy view

    <img src="image/solargraph_usage_example1.png" alt="solargraph_usage_example1" style="zoom:50%;" />
    
- And some other cool things

After installing this extension, we can find that it is not working as intended. 

> If we see a popup message with a nice little *Install* button, ignore it. 

This is totally right, because in its description, it says we also need to install its language server to make it work. 

> The mechanism of VS Code *IntelliSense* and the function of VS Code language server is not to be discussed here, but we ca just think the following gem is an essential module. 

Type the following command to install the gem: 

<a name="sg"></a>
```shell
sudo gem install solargraph
```

> In the description page of *Ruby Solargraph*, `sudo` command is not necessary, but just in case. 

### For WSL users

you might get an error

<!--TODO-->

If we go to the designated directory and have a look at the log file, we will find this: 

<!--TODO-->

It is missing a dependency called `zlib` which is used to build an executable. 

> I don't know exactly what `zlib.h` is, but it doesn't hurt to install it. 

Here is a solution from [*Stackoverflow*](https://stackoverflow.com/questions/18148075/compilation-error-missing-zlib-h)

```shell
sudo apt install zlib1g-dev
```

Try <a href="#sg">this command</a> again, now we should be fine. 

> If you get any error message other than this, go up to the top of this paragraph, do exactly as I did for this problem and get clue from the log file. 
>
> *<a name="wisewords"></a>Google* (in my case, [*DuckDuckGo*](https://duckduckgo.com)) and *Stackoverflow* is your best teacher. 

### For Mac users

You can just ignore this part. 

### For Linux (*Ubuntu*) users

If you encounter any problem, go to the [Windows](# For WSL users) section to find out possible solutions. 

## We are done

This is the end of advanced *Ruby* language support. 

Restart *VS Code* to make *Solargraph* language server running. 

We can find something like this: 

<img src="image/sg_demo.png" alt="sg_demo" style="zoom:50%;" />

## Some noticeable drawbacks

- After the code document is loaded in to the editor, *Solargraph* will not take effect immediately. In fact, there is a little loading icon on the status bar like this:

    <img src="image/solargraph_loading.png" alt="solargraph_loading" style="zoom:50%;" />

> **Important Note: **
>
> If the language server cannot be setup, there must be something wrong with your installation steps. Go back and check the [previous steps](# Set up IntelliSense)

> *IntelliSense* is supposed to be working after the language server is successfully set up. 
>
> However, it is very common that *Solargraph* will **take even more time** to completely work. And to be honest, I am not quite clear about the reason. 
>

- *Solargraph* can fail to parse the code file at anytime, for any length of durations. I don't know the exact reason neither. But, when it fails to work, 

    1. Check if there is any syntax errors in your code file
    2. If not, *please just accept it*. It might go live again after **a few moments**. 

    You will still be able to use the suggestions powered by the *Ruby* extension mentioned above. 
    
---

# Debugging

As we can see, there is a *Debug* tab near main editor window. 

<img src="image/dbg_tab.png" alt="dbg_tab" style="zoom:33%;" />

Ignore it for now. 

The following solution has nothing to do with neither *VS Code*, nor `ruby -r debug`

> Probably because `-r debug` don't cope well with *VS Code*

We will be using [a solution using `ruby-debug-ide`](https://dev.to/dnamsons/ruby-debugging-in-vscode-3bkj)

## Get something installed

### Ruby Debug IDE

Type in this command:

<a name="rdi"></a>

```shell
sudo gem install ruby-debug-ide
```

> Again, `sudo` is not compulsory for some people. 

If you are lucky enough and don't get any errors, jump directly to the [following section](# Debase)

For most people (presumably), we get an error again, very unsurprisingly:

<!--TODO-->

So let's install `rake`

> I have no idea what `rake` is just as you do. 

Here is the [solution](https://github.com/ruby/rake)

```shell
sudo gem install rake
```

Try <a href="#rdi">this command</a> again, and now should be fine. 

> If you are really really unlucky and happened to have other weird errors (especially for *Mac OS* users), get some **Fearless Ideas** and <a href="#wisewords">Do these steps</a>

### Debase

Type in this command:

```shell
sudo gem install debase
```

> If we have no error on output, we are done for this part. 

## Configure *VS Code* debugger

> To be precise, *VS Code* don't have its debugger. In contrast, it provides a graphic interface for language-specific debuggers. 

### Create configuration files

1. Go to the debugger tab, and click *Create a `launch.json` file*
2. Select *Ruby* as environment
3. Select *Listen for `rdebug-ide`*

> Do not change the configuration file if you don't know what these means. 

> **Optional**
>
> We can insert a breakpoint in the code file to see the debug interface. 

## Run the Debugger

> The debugger actually has 2 parts:
> 
> - The user interface
> - The debug server

### Start the server

The server **must be started BEFORE** the listening process, by typing in this:

```shell
rdebug-ide --host 0.0.0.0 --port 1234 --dispatcher-port 26162 /path/to/the/file.rb
```

### Start the debug interface

Just click the button:

<!--TODO-->

**IT IS WORKING!!!**

<!--TODO-->

This is the end of this tutorial. 

> If you like it, star it. 

Thank you, everybody. 