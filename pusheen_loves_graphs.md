## Pusheen Loves Graphs
There is a file Pusheen and a text 
```
Pusheen just loves graphs, Graphs and IDA. Did you know cats are weirdly controlling about their reverse engineering tools? Pusheen just won't use anything except IDA.
```
So, the first thing I did was to get info about the file using the commands file and exiftool. Pusheen turned out to be an ELF executable file. I tried to find the flag by using strings | grep HTB, but there was nothing interesting.
I tried ```objdump --disassemble-all Pusheen | cat -n | tail -n 3``` and there was more than 49k lines of code. It would be strange for an easy task to read all of it. 
I saw IDA reverse engineering tool in the text, so I downloaded it and opened Pusheen. There was an error that graph couldn't be open because of count of elements (more than 1k). But Pusheen loves graphs, so I increased this value in settings to 10k, opened graph overview window and there was the flag.