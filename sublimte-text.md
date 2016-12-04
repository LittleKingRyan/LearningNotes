# Setting Up Sublime Text Workflow

If coding is an essential part of your study and work,
then spending some time (~30 min) setting up the code
editor is definitely worthwhile.

If you are also thinkinig about using Sublime Text 3,
the following resources might come handy:

https://www.youtube.com/watch?v=zVLJfrIwEP8&t=0s
This video includes some of the major features like
Package Control, Color Theme, Emmet, etc.
The guy who made this video is awesome, by the way.

Being able to write and execute snippets of code inside
of Sublime Text not only saves us from switching between
different windoes but also allows us to focus on the code
that we write. To do this with JavaScript, please refer
to this link:
http://www.wikihow.com/Create-a-Javascript-Console-in-Sublime-Text
In particular, if you're thinking about Method 2 with
node.js, replace the code in step 3 with the following
if you have set the path when installing node.js to
usr/local/bin/node
'''
{
    "cmd": ["/usr/local/bin/node", "$file", "$file_base_name"],
    "working_dir": "${project_path:${folder}}",
    "selector": "*.js"
}
'''

