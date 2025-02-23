# Reccurent neural network

In the process of designing systems that can adapt and learn patterns we explore on a basic, fundamental, level theories about how complex biological systems, such as human brains, work. I find this very fascinating. A recurrent neural network is a system that contains feedback loops and can store information from the past. 
This is necessary in order to model long-term dependencies such as can be found in natural language processing. 

This program will learn to produce text similar to the one that
it has been training on using a LSTM network implemented in C. The repo is inspired by Andrej Karpathys <i>char-rnn</i>: https://github.com/karpathy/char-rnn but instead implemented in C to be used in more constrained environments.

# Build 

Do you have a mac or a Linux machine? 
In that case it is super easy to download and run.

## Mac or Linux (UNIX types)

Download the program. 
Open a terminal window and type:

<pre>
# (You may have to install 'git', if you don't already have it!)
git clone https://github.com/Ricardicus/recurrent-neural-net/
cd recurrent-neural-net
# This will compile the program. You need the compiler 'gcc' which is also available for download just like 'git'.
make
</pre>

If there is any complaints, then remove some flags in the 'makefile', I use 'msse3' on my mac but it does not work for my raspberry Pi for example. 

Then run the program:
<pre>
./net datafile 
</pre>

where datafile is a file with the traning data and it will start training on it. You can see the progress 
over time. 

## Windows

I have only built it using Visual Studio Native Tools Command Prompt for VS2017. 

Install CMake and Nmake (and git). 
Then do:

<pre>
git clone https://github.com/Ricardicus/recurrent-neural-net/
cd recurrent-neural-net
cmake -G"NMake Makefiles"
nmake
</pre>

# Configure

Check out the file "std_conf.h".

In std_conf.h you can edit the program. You can edit the hyperparameters such as learning rate etc, set the number of layers (2/3 is best I think), set how often it should output data etc. If you edit this file, you edit the source code and you will need to rebuild the program with the command "make". You can also use input arguments to set some of the behaviour.

Running the program with no arguments triggers the help output to be displayed. This help shows what flags can be
passed as arguments to the program to modify its behaviour. The output looks like this:

<pre>
Usage: ./net datafile [flag value]*

Flags can be used to change the training procedure.
The flags require a value to be passed as the following argument.
    E.g., this is how you train with a learning rate set to 0.03:
        ./net datafile -lr 0.03

The following flags are available:
    -r  : read a previously trained network, the name of which is currently configured to be 'lstm_net.net'.
    -lr : learning rate that is to be used during training, see the example above.
    -it : the number of iterations used for training (not to be confused with epochs).
    -mb : mini batch size.
    -dl : decrease the learning rate over time, according to lr(n+1) <- lr(n) / (1 + n/value).
    -st : number of iterations between how the network is continously stored during training (.json and .net).
    -out: number of characters to output directly, note: a network and a datafile must be provided.

Check std_conf.h to see what default values are used, these are set during compilation.

./net compiled Feb 14 2019 14:41:42

</pre>

The -st flags is great. Per default the network is stored upon interrupting the program with Ctrl-C. But using this argument, you can let the program train and have it store the network continously during the training process.
In that case the network is avaiable for you even if the program is unexpectedly terminated.

Enjoy! :)

# Examples
I trained this program to read the first Harry Potter book, It produced quotes such as this: 

"Iteration: 303400, Loss: 0.07877, output: ed Aunt Petunia suggested
timidly, hours later, but Uncle Vernon was pointing at what had a thing while the next day. The Dursleys swut them on, the boy. "

It has definately learned something. 

For more activity based on this neural network, check out my twitter bot: 
https://twitter.com/RicardicusPi


# Comments

For now I have just started with the implementation.

I figured if it was to be implemented in C instead of Python then
there would be a huge speedup which the results show!

I will give this some time and hopefully I figure out a way that
optimizes the program even more for speed.. Until then, have a go at this 
little program and edit it as you please! 

# Build

I use GCC and compile with with: 
gcc *.c -O3 -Ofast -msse3 -lm

Try to optimize it the way you want using the compiler at hand!

# Additional interesting stuff

Under the folder 'html' you will find a document that can be used to play around with pre-trained models. 

Below is an image of this GUI and how one can interact with it. 

<img src="https://raw.githubusercontent.com/Ricardicus/recurrent-neural-net/master/html/Screendump_example.png"></img>

In the image of the GUI above, we see that a word is about to be formed starting with the letter <i>i</i>. The most likely words to be formed are: <i>if</i>, <i>in</i> and <i>it</i>. 
