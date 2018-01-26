# Assignment 2:  Share forked copy by 1/27/18
Assignment will be 2 will be turned in via your github account.  Please fork, assignment 2 from trgn510.  You can then edit inline at github.  We won't be doing a markdown style yet, but why not try that? Its very nice! You can essentially copy and paste into the README your answers after testing them in the server, replacing the key text.  Analysis must be completed on the server trgn510.pmed.io, and will be used to help assist you in case of issues.   The directory tree must be proper per the assignment.  I'll review your github and the server.

There are different code blocks, those with black text are for you to paste into the command line terminal and observe what happens.  It may create a directory tree, and if this tree isn't created that part of the assignment is not done.  For example:

echo "This is a command to put into the server, and its in a code block on this webpage. If the text is red code block, then it is the result of the command, and you shouldnot paste it in"
If the text is red code block, then it is the result of the command, and you should not paste it in".  You'll notice a "#" there which is way to insure that its something that doesn't get interpreted by bash when provided to the bash shell.

Do not put me in the command-line, the red indicates a result and I just want to show you it.
They'll be places you are expected to substitute a line for the answer. These are green and codeblocked and begin and end with a *. IMPORTANT, to do this.

*Replace me with answer*
We then replace the answer with "**" before and after "**". How many?  Two asterisks before and two after. Why - take a look at markdown.

**Varsha Giri**

## 1. Logging in
Please login to trgn510.pmed.io and verify that you are in trgn510.pmed.io using hostname.

**hostname** 
## 2. PATHs and organization.
There are lots of environmental variables loaded into bash through .bashrc.  One is the $PATH variable.  Any executables within these folders do not require typing a path to run.  For example below we see all the paths where our executables without a path can be located.  In a step below we extend it.

echo $PATH
#/usr/local/bin:/usr/local/mysql/bin:~/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/davidcraig/.local/bin:/home/davidcraig/bin
ls is program that lists files.  Where is it located?

whereis ls #ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz
So this tells us the path of ls.  There are a few notes on path.  cd ~ takes us to our home directory.   We can see what our home directory is with "pwd".   "." is a shortcut for local directory. ".." is one directory up.  What is the path of our home directory?  Note that below, I am using ';' to put two commands together. ';' means end of line in bash.

cd ~;pwd
This shows that "/user/trgn510" is our home directory - though you will have a different directory.  Next-gen sequencing is big data - terabytes and petabytes.   Usually you have many different drives.  We can see the mounted drives on a system by typing 'df -h'.  The result of this is below.  We can see that /user is on a partition of data that has 99Gbytes, and 2% is used.

Lets create a local "bin", using mkdir bin and lets create an assignment folder.  Lets also set up our work environment.  Then I'd like you to list it out

cd ~
mkdir -p bin projects/assign2
export PATH=$PATH:~/bin
cd projects/assign2~
**cd ~;
ls -R** 

## 3. Shared infrastructure
who
Take a look in your terminal, ok what are those users up to.  Lets find out with w

w
What are all processes, lets type top to find out.  Remember control c to get out of that screen.

top


Ok - that's too many people who have logged on, lets just pipe it to tail to see the last 5 people

last | tail
What if we wanted the first 5 lines - there must be a way to take the head of a file, such as the first 5 lines.

**last | head -5**

## 4.  Our network
I wonder if this server can see the internet.  Can it see google. Lets ping Google with a little message and see how long it takes to respond.

ping -c 5 google.com
This provides the time - and is one indicate of the network.  If things are slow, you can ping and check the time to respond.  Lets scrape a web page.  Lets actually get someone's genome. Please go to this page: ftp://ftp-trace.ncbi.nlm.nih.gov/giab/ftp/release/NA12878_HG001/NISTv3.3.2/GRCh37/

Copy the link to download the file "HG001_GRCh37_GIAB_highconf_CG-IllFB-IllGATKHC-Ion-10X-SOLID_CHROM1-X_v.3.3.2_highconf_PGandRTGphasetransfer.vcf.gz".  On your server, download this by typing wget and the full path of the URL.

**wget ftp://ftp-trace.ncbi.nlm.nih.gov/giab/ftp/release/NA12878_HG001/NISTv3.3.2/GRCh37/HG001_GRCh37_GIAB_highconf_CG-IllFB-IllGATKHC-Ion-10X-SOLID_CHROM1-X_v.3.3.2_highconf_PGandRTGphasetransfer.vcf.gz**

## 5.  Example by a person's genome.
This is the pretty much the genome that has been sequenced by the most platforms the most times, and for which we have identified with highest confidence the genetic variants in that person.  The file ends in ".gz", which means it is zipped.  Unzip it

gunzip HG001_GRCh37_GIAB_highconf_CG-IllFB-IllGATKHC-Ion-10X-SOLID_CHROM1-X_v.3.3.2_highconf_PGandRTGphasetransfer.vcf.gz
This made it plain text readable.  You can preview file using "less", please do that knowing you jump around using vim commands such as control-F.  We notice there are many lines that begin with a "#" forming the header.  We then get to variants which have a format specified in the VCF4.2 spec.  Please paste below the command to download via wget on the server the Spec for VCF 4.2.  You should have wget URL, where URL is the URL of a PDF file.

**wget https://samtools.github.io/hts-specs/VCFv4.2.pdf**

## 6.  File sizes, and compression.
What is the size of the uncompressed file and what is the size of the compressed file

**du -h HG001_GRCh37_GIAB_highconf_CG-IllFB-IllGATKHC-Ion-10X-SOLID_CHROM1-X_v.3.3.2_highconf_PGandRTGphasetransfer.vcf.gz**

**du -h HG001_GRCh37_GIAB_highconf_CG-IllFB-IllGATKHC-Ion-10X-SOLID_CHROM1-X_v.3.3.2_highconf_PGandRTGphasetransfer.vcf**

That's a fair amount of space.  How much space do we have to work with.  Type 'df -h' to find out.

## 7.  Grep it up
How would we create a file that only includes variants.  Well 'grep' is a hand command.  We can grep out all reads that don't start with a "#".  grep with the "-v" flag would do it, and we could put that in a file...  Please do so.

grep -v "^#" HG001_GRCh37_GIAB_highconf_CG-IllFB-IllGATKHC-Ion-10X-SOLID_CHROM1-X_v.3.3.2_highconf_PGandRTGphasetransfer.vcf > NA12878.variants.vcf
How many variants are in the file?  The standard tool to count the number of lines is call 'wc', however you need to actually put a flag for lines.

**wc -l NA12878.variants.vcf**

Lets look at the contents again using something like more, less, or head (type less and the VCF file name).  We see a space or tab delimited file with chromosome, position in the genome,  the name of a variant if it has a name (dbSNP), the reference base(s), the base in the person or so called alternative base, a quality score, a field saying whether this variant PASS or has another filter field, a series of semi-colon delimited informational fields that are variable in number by line, a field which describes later fields providing genotype.  That field is colon delimited.  We then see a field which gives the genotype for a person, identifying if they have two or one copies of the variant.  If we are using less to view the file, we can see what the space like character is.  Simply, type forward slash (/), and the space character.  You should see spaces highlight.  If we wanted to see tabs, we need to type "control-v", and then the tab character.  We can also see that it is a variable number of spaces.



We can review the spec, but notably if we wanted to see the header, we could type

grep "^#CHR"

#CHROM POS ID REF ALT QUAL FILTER INFO FORMAT HG001

This is a lot of info, and us learning about the VCF file is not going to be the objective of the course.  More importantly, this is just a simple table.  Its a table within tables, and something where we might need to pull things out.

## 8.  Cut and cut more.
What chromosomes are there?  This is column 1.  Lets

Lets see if they are male or female.  If they are female we should see "X" variants be heterozygous, that is because there are two copies we see a 0/1 where they have a single copy of a variant.  Males would be always hemizygous.    Lets use 'cut', which has syntax in part as follows 'cut -d "delimiter" -f (field number) file.txt'.  Please use 'cut' to create a column of chromosome calls.  Now if we know its tab delimited, how do we make a tab.  Often we can \t

cut -d "\t" -f1 HG001_GRCh37_GIAB_highconf_CG-IllFB-IllGATKHC-Ion-10X-SOLID_CHROM1-X_v.3.3.2_highconf_PGandRTGphasetransfer.vcf | head #cut: the delimiter must be a single character #Try 'cut --help' for more information.
Ok - fail.  Another option is by control-v then 'tab'.  That creates a single character that you can't see which is encoded by a tab and not a space.

`cut -d "<control-v + tab" -f1 NA12878.variants.vcf | head`
Did you notice we piped to head?  If you don't do that you'll be waiting for 4 million numbers to go by.  However, what we want is the unique or distinct numbers.  Instead of piping to head what can we pipe to so the output is only the chomosomes?  Ok - the goal of this course is to teach you how to use all languages and comamnds to quickly get to the goal, so google it. Look for a way to print unique results, and sort will probably be involved.  One command, but several pipes.

**cut -f1 NA12878.variants.vcf | uniq**
The result should be this

 
I don't see Y this must be female.  Maybe we should double check.  If they are female we should a fair number of heterozygous X calls, and males will be hemizygous.  We know that the genotypes are in the 10th column.  We can pull that out with cut again.

`cut -d " " -f 10 NA12878.variants.vcf | head`


Ok.  That's not quite what I am looking for.  I just want the genotypes.  Instead of head, can you pipe the above result into another pipe, grabbing the first field?

**cut -d " " -f10 NA12878.variants.vcf | cut -d ":" -f1**


Ok, first what are the "0/1" vs. 0|1 and so forth? This information is in the header. Find out using more and the original file.  Lets count the number of "0|1".  How do we count the number of unique genotypes?  Make sure you understand the command that's helping here - you might need to make sure they are sorted.

**cut -d " " -f10 NA12878.variants.vcf | cut -d ":" -f1 | sort | uniq**

## 9.  Python scripting
If we look at our file, we really have tables in tables.  The info column is column 8.  We've been doing a lot of bash scripting.  We know how to make a bash script.  Lets switch languages and introduce python.  Now - you might hear about perl - but perl isn't just a dead language its a zombie language used by bioinformaticians from the 90s.  Once you learn perl, you won't learn anything else so lets start you on the right foot.  Learning python as the 10th problem of the second assignment, sounds ambitious - but they teach programming to 8 year olds in hour, so why not graduate students.  Basically, instead of #!/usr/bin/bash as the first line, we will do #!/usr/bin/py.  Please create your first python script by typing "vim command.py". 
command.py

```python

#!/usr/bin/python

import sys

print 'Number of arguments:', len(sys.argv), 'arguments.'
print 'Argument List:', str(sys.argv)
```

Lets explain this.  The first line tells us that python will run the remaining lines.  The second line imports a library.  This library places those command-line arguments in an array called sys.argv.  Arrays are basically numbered variables - that is the arguments are... sys.argv[0], sys.argv[1], and so forth.  Or we just refer to the whole lot as sys.argv.  Note that often, computer languages start counting with "0".  len() is a function that essentially operates on an array, len(sys.argv), if we google it tells us how many items there are.  str() just turns them into a single concatenated sequence.

We have command.py, but we have not made it executable.  Please change the permission such that we can run command.py.

**chmod 755 command.py**

Now that's executable, we can test it out as we do below, typing './command.py', recognizing that command.py is not in our path, and we must give then the path.  We do this with "./" before the name when we are already in the correct directory.



## 10. Python regexing.
We can do complex search and replace, and that is called regular expressions.  Regular expressions are awesome!  These can get unbelievably complex tasks super easy.  Historically, people did these with sed and nawk.  A lot of people struggle with these, and nobody hires people who put sed/nawk on their CV.  So our focus will be using regex via python.

Lets go to our ~/bin directory and create a new command to help us with regex.

cd ~/bin
Lets now edit and create our new python script, pymatch.py.  Please note the indentation is essential, so if you lose it during the copy and paste do manually put them back in.  Indents basically, tell us what is being looped, such as in a for statement.

pymatch.py

```python

#!/usr/bin/env python
import sys, argparse, re # Import librarys

#initiate parser
parser = argparse.ArgumentParser()
parser.add_argument("-r", "--regex", help="match by regular expression")
parser.add_argument("-f", "--file", help="match by regular expression")
parser.add_argument("-o", "--options", help="match by regular expression")
args = parser.parse_args() # parse the above rules, store them in args.

# read arguments from the command line args.file if this exists, otherwise just take what is streaming
if args.file:
    data = open(args.file,"r")
else:
    data = sys.stdin

if args.regex and data: # If args.regex exist and data exist
    for line in data: # Loop through data, assigning to line
        matches = re.findall(args.regex, line) #findall matches, store in matches
        if matches:
            print matches
```

Lets review this python program.   We will use the sys and argparse for helping us with command line arguments.  We will use the regex or 're' module too.  argpas is module containing functions, and one "ArgumentParser()" helps us get the arguments out of a command line in "argument" "value" pairs.

Essentially, we add the rules (or arguments attributing the short-name, long-name, and help description.  We then parse all of these into an associative array.  An associative array is an array where we bin by text name, not number.  This instead of args[0], we see args.match where a period separates, instead of brackets.

  We do see the first use of a conditional - one of the most important concepts - and if statement.  Conceptually a condition is if (statment is true), do {these commands}, else, do {these commands}.

LETS TRY IT OUT, please change the permission to 755, and run it.  If you have it in your bin no command is necessary.

echo ";gene_symbol=PTEN;gene_name=phospho;gene_sequence=atc;" | match.py -r "gene_symbol=(.*?);"
`[('PTEN')]`

So lets try just two last commands. If you need help, you can check out regex101.com

**echo ";gene_symbol=PTEN;gene_name=phospho;gene_sequence=atc;" | pymatch.py. -r "gene_name=(.*?);"**

**echo ";gene_symbol=PTEN;gene_name=phospho;gene_sequence=atc;" | pymatch.py. -r "gene_name=(.*?);gene_sequence=(.*?);"**
 

Pages: 1 2 3 4 5 6 7 8
