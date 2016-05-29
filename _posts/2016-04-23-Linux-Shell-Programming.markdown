---
layout: post
title: "Linux Shell Programming"
date: 2016-04-22 10:30:00
---

Also there are some programming language such as Python, Perl and Ruby could help to take the job of Linux system programming but you still need to know something about Bash.

OK Let's kick start!

# Print the environment variable
You can use `echo` and `printf` to display some environment variable on the screen.
{% highlight bash %}
echo $JAVA_HOME
echo ${JAVA_HOME}
#both are same will print your java home path
printf "%s\n" $JAVA_HOME
printf "%-10s\n" ${JAVA_HOME}
#printf is same with C programming language
{% endhighlight %}

# Calculation
In Bash shell, `let`, `(())` and `[]` can be used for basic calculation.
{% highlight bash %}
a=4 #there should be no space around the `=`
b=5
let result=a+b #no '$' while using let
echo $result
{% endhighlight %}

# Stdin
`>` and `>>` are for file input.
{% highlight bash %}
echo "This is test" > temp.txt  #This will replace the content of temp.txt
echo "This is test2" >> temp.txt #This will append
{% endhighlight %}

# Date format
In Unix-like system, date is stored as a number which record the count of seconds from Jan-1 1970 UTC
{% highlight bash %}
date # Sun Apr 24 11:49:52 CST 2016
date +%s # 1461469825 %s for the Unix seconds
date "+%d %B %Y" # 24 April 2016
date +%D # 04/24/16 mm/dd/yy
{% endhighlight %}

# Function and param
Like other script language, Bash also support function.
{% highlight bash %}
#define a function
function name()
{
  statements;
}
#or
name()
{
  statements;
}
# to execute a function
name ;
name arg1 arg2 ;
{% endhighlight %}

# Pipes
Pipes let you use the output of a program as the input of another one.
{% highlight bash %}
$ cmd1 | cmd2 | cmd3
#The output of cmd1 will pass to cmd2 and the output of cmd2 will send to cmd3 as input
$ ls | cat -n > out.txt
#The current directory will pass to cat -n, and cat -n will be the input stdin then redirect to out.txt
{% endhighlight %}

# Cat command
`cat` command is used for contact the display content.
{% highlight bash %}
#remove the space
cat -s file
#add line number
cat -n file
{% endhighlight %}
`cat` won't modified your file content, just create a new one in stdin.

# Translate
`tr` used for replace and delete character from stdin.
{% highlight bash %}
echo "HELLO WORLD" | tr 'A-Z' 'a-z' # hello world
echo 12345 | tr '0-9' '9876543210' # 87654 replace
echo "Hello 123 world 456" | tr -d '0-9' # delete digit
{% endhighlight %}

# Checksum
MD5
{% highlight bash %}
md5 filename # MD5 (filename.txt) = 9acef9a7ca1069a763da26c7c4879f7c
md5 -s "Hello World" # MD5 ("Hello World") = b10a8db164e0754105b7a99be72e3fe5
{% endhighlight %}

# File rename and moving
Here's an example for rename all the mp3 file in current directory.
{% highlight bash %}
count=1;
for file in *.mp3
do
new=sound-$count.${file##*.}
mv "$file" "$new" 2> /dev/null
if [ $? -eq 0];
then

echo "Renaming $file to $new"
let count++

fi
done
{% endhighlight %}
The output will be like beflow
{% highlight bash %}
Renaming A.mp3 to sound-1.mp3
Renaming B.mp3 to sound-2.mp3
Renaming C.mp3 to sound-3.mp3
{% endhighlight %}

# Word Count
{% highlight hash %}
wc -l file # the line number
cat file | wc -l # use cat as stdin
wc -w file # the word number
wc -c file # the char number
{% endhighlight %}

# Print the directory tree
{% highlight hash %}
tree dirname
tree -h # print the file and size
{% endhighlight %}

# Download the website
`wget` is used for file download. If you are using the Mac OS, you need to download the command first.
{% highlight bash %}
wget URL
wget URL1 URL2 URL3
wget -t 5 URL # retry 5 times
wget -c URL # continue getting a file
{% endhighlight %}

`curl` is same with the `wget` command, but it will create the stdin stream as input.
{% highlight bash %}
curl URL
{% endhighlight %}

# A file crawler
Get pic from the website
{% highlight bash %}
if [ $# -ne 3];
then
  echo "Usage: $0 URL -d DIRECTORY"
  exit -1
if

for i in {1..4}
do
  case $1 in
  -d) shift; directory=$1; shift ;;
  *) url=${url:-$1}; shift ;;
esac
done

mkdir -p $directory;
baseurl=$(echo $url | egrep -o "https?://[a-z.]+")

curl -s $url | egrep -o "<img src=[^>]*>" |
sed 's/<img src=\"\([^"]*\).*/\`/g' > /tmp/$$.list
sed -i "s|^/|$baseurl/|" /tmp/$$.list

cd $directory;

while read filename;
do
  curl -s -O "$filename" --silent
done < /tmp/$$.list

##usage: ./img_downloader.sh url -d dir
{% endhighlight %}

# Command execution time
Using `time` command before any command
{% highlight bash %}
time ls
#cmd_outp.sh	file_sum.md5	variables.sh
#
#real	0m0.010s  wall clock time
#user	0m0.002s  user mode CPU time
#sys	0m0.005s  kernel mode CPU time
{% endhighlight %}
