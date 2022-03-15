# Scripting with Bash

cat ip.tx | grep "64 bytes" | cut -d " " -f 4&#x20;

grep searches for results that have 64 bytes in the line&#x20;

cut -d -d is used as a delimiter&#x20;

if -d option is used then it considered space as a field separator or delimiter this will result in the terminal outputting &#x20;

to get rid of the **:** cat ip.txt | grep "64 bytes" | cut -d " " -f 4 | tr -d ":"
