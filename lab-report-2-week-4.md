# Lab 2 Report CSE 15L

***

In this lab, we worked with a file *MarkdownParse.java*, which attempted to parse a Markdown file and print out all the links in the file. If you are curious, this is what it looks like. 

![OriginalCode](lab2-1.png)

Unfortunately, this code doesn't do exactly what we want. Let's try and find ways we can break this code, and then fix it!


***

For starters, it looks like this code is not differentiating between links and images. Let's try and running MarkdownParse on this file to test this theory -  [image.md](https://raw.githubusercontent.com/TheZenMasterz/markdown-parse/main/image.md)

When we run the command(after compiling MarkdownParse.java), ```java MarkdownParse image.md```, our program prints out ```[google.com, pic.png]```. We don't wan't it to print out pic.png, so it looks like we were right. 

Now, we need some way to be able to differentiate between links and images. Lucky for us, there is a ! in front of the open bracket for images. All we need to do in our program is, before we add something to our array of links, we check to see if it has that ! before the open bracket, and if it does, don't add it to the array. 

![](codeChange1.png)

Now let's try running it again. This time the program outputs just ```[google.com]```. It worked!

In this case, the bug was the program not checking if what it was adding to the array of links was an image. The bug resulted in the symptom that the program outputting images as links. We could produce this symtom by inputting in a markdown file with an image. 

***

Let's try looking for another bug! How about, if we try inputting in a file that isn't valid - [incorrect.md](https://raw.githubusercontent.com/TheZenMasterz/markdown-parse/main/incorrect.md)

What happens when we run ```java MarkdownParse incorrect.md``` ? Our program prints out ```Exception in thread "main" java.lang.StringIndexOutOfBoundsException: begin 18, end -1, length 28```. We don't want our program to crash, we just want it to print out the links. 

Since the link in this program isn't a valid link, how about we just don't add it to our array of links? Let's just add a check to see if there is actually a closed parentheses anytime we're adding a link!

![](codeChange1.png)

Time to check if it works. Let's run it on incorrect.md again. Our program outputs ```[]```. Perfect! It didn't output any links. 

So, the bug of the program not checking for the existence of a closed parentheses was causing the symptom of an IndexOutOfBoundsException. We produced this symtom by inputting in a file where there is a link without a closed parentheses. 

***

Hmmm, this is so much fun, let's see if we can't find one more bug. What if we input another incorrect file, this time with no brackets at all. How about this file - [incorrect2.md](https://raw.githubusercontent.com/TheZenMasterz/markdown-parse/main/incorrect2.md)

Let's try running ```java MarkdownParse incorrect2.md```. Hmm, our program outputs ```Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: -2```. 

How about we try a similar fix to last time and just check for the existence of a next open and closed bracket. If there are none left, there are no links left to find.

![](codeChange1.png)

Hopefully this will work. Let's run it on incorrect2.md again. Our program outputs ```[]```. Our program didn't output a link. Exactly as intended!

So, in this instance, the program had a bug in that it never confirmed the existence of brackets before a link. The symptom was another IndexOutOfBoundsException. We could produced this symtom by inputting in a file without brackets. 

***

There are still even more errors to discover in *MarkdownParse.java*, and while I could look for more all day, I think I might just go eat lunch instead. If you want to take a look though, be my guest. It's fun, I promise. 