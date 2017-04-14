# Problem

When I open a new terminal I am not located where my project source code is. On top of that, sometimes I navigate away from that directory for one reason or another and then in order to open another project I have to go back to my _project_ directory before typing in `subl .`.

# Solution

I wanted to learn shell scripting for awhile, and I am not a fan of contrived exercises. I thought this was a solid practical
command that would alleviate an annoyance in my daily life. Thus, I learned some shell scripting and wrote a command that I
use both my on my personal MacBook and work one. 

I set it up so that no matter where I am in the terminal all I need to do is type `code_src` followed the project. I 
also decided to make it so that I do not need to type in the whole project name only part of the folder name.
