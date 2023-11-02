# Smallchat

TLDR: This is just a programming example for a few friends of mine. I upload a video on my YouTube channel [zooming into the code](https://www.youtube.com/watch?v=eT02gzeLmF0), to see what can be learned from a so simple and broken (on purpose) example.

And now, the full story:

Yesterday I was talking with a few friends of mine, front-end developers mostly, that are a bit far from system programming. We were remembering the old times of IRC. And inevitably I said: to write a very simple IRC server is an experience everybody should do (I showed them my implementation written in TCL; I was a quite shocked that I wrote it 18 years ago: time passes fast). There are very interesting parts in a program like that. A single process doing multiplexing, taking the client state and trying to access such state fast once a client has new data, and so forth.

But then the discussion evolved and I thought, I'll show you a very minimal example in C. What is the smallest chat server you can write? For starters to be truly minimal we should not require any proper client. Even if not very well, it should work with `telnet` or `nc` (netcat). The server main operation is just to receive some chat line and send it to all the other clients, in what is sometimes called a fan-out operation. But yet, this would require a proper readline() function, then buffering, and so forth. We want it simpler: let's cheat using the kernel buffers, and pretending we every time receive a full-formed line from the client (an assumption that is in the practice often true, so things kinda work).

Well, with this tricks we can implement a chat that even has the ability to
let the user set their nick in just 200 lines of code (removing spaces
and comments, of course). Since I wrote this little program as an example for
my friends, I decided to also push it here on Github.

## Preparation
1. Install gcc and make
2. Clone this repository
3. Install nc (netcat) if you don't have it

## Usage 
1. Run `make` in your terminal, to compile the program, you will need gcc and make installed,and you will get a file called `smallchat` in the same directory.
2. Run `./smallchat` in your terminal, you will start a server on port 7711.
3. Open another terminal and run `nc localhost 7711` to connect to the server. Input `/nick yourname` to set your nickname, and then you can chat with others.

The susseccful output will be like this:
![](https://cdn.studyinglover.com/pic/2023/11/ec426ea656b4bd41bab7f5fcb559d54f.png)