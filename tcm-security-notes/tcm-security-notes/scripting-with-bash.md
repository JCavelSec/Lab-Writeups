# Scripting with Bash

cat ip.tx | grep "64 bytes" | cut -d " " -f 4 grep searches for results that have 64 bytes in the line cut -d -d is used as a delimiter if -d option is used then it considered space as a field separator or delimiter this will result in the terminal outputting  to get rid of the **:** cat ip.txt | grep "64 bytes" | cut -d " " -f 4 | tr -d ":"
