less || man

## less Command in Linux
---

Have you ever tried to open a large, multi-page text file in the terminal?

The contents whizz past you, and you can only see the last few lines. The less command in Linux addresses the inconvenience of reading large text files. It allows users to view the file contents screen by screen (or page by page).

In Linux, the less command is similar to the more command but offers additional features. For instance, it can scroll up and down through the file, search for specific text, and navigate to specific line numbers.

This guide provides a detailed overview of the less command in Linux. We’ll explore its usage, options, and 10+ examples to help you develop a better understanding.

Let’s start with the background of the less command.

Table of Contents

Interesting Background of less Command
The Basics of Using the Less Command
Popular Options of the less Command
Common Commands to Use With less in Linux
How to Navigate with less Command in Linux Text Files
How to Use the less Command in Linux
Prerequisites
Example #1: Open a Text File
Example #2: Show Line Numbers
Example #3: String Search
Example #4: Pattern Search
Example #5: Remove Multiple Blank Lines
Example #6: Open Multiple Files Concurrently
Example #7: Set Bookmarks in Text
Example #8: Keep Content On Screen After Exit
Example #9: Real-Time File Monitoring
Example #10: View Piped Input
Example #11: Edit Files
Example #12: Access File Statistics
Conclusion
FAQs
Interesting Background of less Command

The less command, created by Mark Nudelman between 1983 and 1985, is an upgraded version of the more command used in Unix.

It was named less as a playful contrast to more because it lets users scroll forwards and backward through text files. Initially made for Unix, it’s also used in other operating systems like all major Linux distributions and Windows.

The Basics of Using the Less Command

Using the less command in Linux is pretty straightforward. You type less followed by the file name you want to read. For instance, typing less filename.txt opens the file in a view where you can scroll up and down through the text.

You use the arrow keys to navigate, and q to quit and return to the command line. It’s a simple way to view and scroll through long files without opening them in an editor.

Here’s the basic syntax for this command:

# less [options] filename

In this command, [options] modify how the less command displays the file content. Executing the command without any options will present the file’s contents in standard format.

You can see a concise version of the options and flags of the command by entering –help with the less command (as shown below).

# less --help

# less --help

Also Read: 13 Examples That Showcase the xargs Command in Linux

Popular Options of the less Command

Below is a table of popular options for the less command in Linux.

Popular Options of the less Command

Common Commands to Use With less in Linux

Common Commands to Use With less in Linux

How to Navigate with less Command in Linux Text Files

The less command in Linux offers improved text file navigation through diverse keyboard shortcuts. It is particularly beneficial for going through large files.

You can use the following shortcuts to navigate the document in the less command:

Down Arrow, Enter, e, j: Moves forward by one line.
Up Arrow, y, k: Moves backward by one line.
Space bar, Page Down: Advances forward by one page.
Page Up, b: Moves backward by one page.
Right Arrow: Scrolls the view to the right.
Left Arrow: Scrolls the view to the left.
Home, g: Jumps to the beginning of the file.
End, G: Jumps to the end of the file.
/[string]: Searches forward for the specified string.
?[string]: Searches backward for the specified string.
n: Finds the next occurrence in a search.
N: Finds the previous occurrence in a search.
q: Exits the less command.
Also Read: lsof Command in Linux with Examples

Also Read: A Guide on How to Install and Use Linux Screen Command in 2024

How to Use the less Command in Linux

Here are some practical scenarios demonstrating the use of the less command.

Prerequisites

Before we begin with examples, let’s review the prerequisites.

A system running a mainstream Linux distribution.
Access to a terminal (Usually accessed with the Ctrl + Alt + T keyboard shortcut).
Example #1: Open a Text File

To view a text file in Linux with less, simply provide the path to the file. For instance:

# less /etc/updatedb.conf

# less etcupdatedb.conf

This command opens the configuration file in less, showing initial lines in the terminal, with file details at the bottom-left.

You can now use the shortcuts we mentioned to move forward or backward, or search for specific text in the file.

Example #2: Show Line Numbers

By default, less doesn’t display line numbers.

If you wish to see the line numbers, use the -N option. This is a great option for files that contain code snippets. Line numbers make finding specific parts in the text easier.

Example Usage:

# less -N /etc/ssh/ssh_config

# less -N etcsshssh_config

Note that every line is sequentially numbered when you open a file with the less command.

Example #3: String Search

 

To find a specific string, press / for a forward search or ? for a backward search and type your term. After entering it, press Enter.

The first match will be highlighted. Press n for the next match or N for the previous one.

For example, after opening a file with (for instance /etc/ssh/ssh_config), type /a to search for a in the file.

The output would look something like the following:

String Search Output

Note that in a backward search, the roles of n and N are inverted: n takes you to the next occurrence towards the start of the entire file in a terminal window, while N moves you towards later occurrences closer to the end.

Example #4: Pattern Search

The -p option in the less command allows you to open a text file directly at the page where the first match of a given search pattern occurs. This search is sensitive to case differences.

It’s worth noting that Linux offers grep as another powerful tool for pattern searching and working with text patterns.

For instance, if you execute the following command, you will find the ssh_conf file open at the first occurrence of the string Forward:

# less -pForward /etc/ssh/ssh_config

# less -pForward etcsshssh_config

Remember, when using the -p option for pattern searches, attaching the pattern directly to the option without any intervening whitespace is essential.

Example #5: Remove Multiple Blank Lines

In the less command, utilize the -s option to merge multiple blank lines in a text file into a single blank line. This functionality is especially useful for enhancing readability by reducing the blank spaces between text. In the case of particularly long files, the -s flag allows more content to be displayed on a screen page.

For instance, consider a file named RedSwitches.txt that contains several blank lines interspersed between lines of text. You can view this file with the following command:

# less RedSwitches.txt

# less RedSwitches.txt

As you can see, the command rendered the file as it is with multiple blank lines. You can combine these multiple blank lines into a single line by applying the -s option with the less command in Linux:

# less -s RedSwitches.txt

# less -s RedSwitches.txt

Example #6: Open Multiple Files Concurrently

The less command lets you open and view multiple files simultaneously while retaining your current position in each file. To do this, list the file names sequentially. For instance:

# less RedSwitches.txt RedSwichesProducts.txt

# less RedSwitches.txt RedSwichesProducts.txt

This command will open both RedSwitches.txt and RedSwichesProducts.txt in less, and you’ll see an indicator at the screen’s bottom showing which file is currently being displayed.

Navigate to the next file using the less command in Linux by pressing the : key and then n.

Navigate to the next file using the less command in Linux by pressing the key and then n.

Switch back to the preceding file in the less command by pressing : followed by p.

Example #7: Set Bookmarks in Text

You can mark important parts in a file with bookmarks.

Setting a bookmark in less is a simple process.

Go to the text you want to bookmark, press m, and choose a letter to designate the bookmark. For setting multiple bookmarks, use different letters for each bookmark.

For instance, open the RedSwitches.txt with the following less command:

# less RedSwitches.txt

Now, press m on the keyboard, and select the sentence you want to bookmark. You’ll see something like the following:

Now, press m on the keyboard, and select the sentence you want to bookmark. You’ll see something like the following

Return to a previously set bookmark in the less command in Linux by pressing m followed by the letter you assigned to that bookmark.

Example #8: Keep Content On Screen After Exit

Typically, exiting the less command clears the displayed file content from the terminal. Use the -X option to override this and keep the file contents visible after exiting.

Consider the following command that keeps the contents of the target file visible even when you exit the less command:

# less -X /etc/ssh/ssh_config

# less -X etcsshssh_config

Example #9: Real-Time File Monitoring

The less command features a real-time monitoring mode that you can activate with the +F (forward) option. This mode allows less to continuously display new messages or lines as they are added to a file.

When the + flag is used, it signals the less command to apply the option as though it were activated from within the command. To enter the forward mode while a file is open in less, simply press the F key.

For instance, to monitor the latest updates in the system log file in real-time, use:

# less +F /etc/ssh/ssh_config

# less +F etcsshssh_config

This command initiates less in forward mode, enabling you to track updates to the file as they occur. While in this mode, less will display a notification awaiting new data and automatically scroll down as new messages arrive.

To exit forward mode and revert to the standard interactive mode of less, press Ctrl+C.

Example #10: View Piped Input

The less command is highly effective for managing the output from other commands, mainly when the output is extensive and could clutter the terminal. This is done through piping.

For instance, the dmesg command, which outputs kernel messages, often generates several screens of data. You can pipe the output into less for better navigation and readability. The example syntax is as follows:

# dmesg | less

Press the End key to refresh the output and view the latest screens. You can also use the +F option or press F while in less to enable automatic update, keeping you abreast of new data as it comes in.

Here’s an example of this approach:

# dmesg | less +F

# dmesg less +F

Here, the output will display the most recent page of the file and wait for new data.

Example #11: Edit Files

Although less is primarily for viewing files, it offers a handy shortcut to switch to editing mode.

Press v while viewing a file in less to open it in the system’s default text editor. Exiting the editor will bring you back to less command’s output.

We strongly recommend using the select-editor command in the terminal before trying out the less command’s edit feature. This allows you to set your preferred editor as the system’s default editor.

Example #12: Access File Statistics

Press = while using less to get detailed statistics about the file, including its location. For a more comprehensive view, initiate less with the -M option for verbose mode, which displays the range of lines currently visible, your progress through the file, and its size.

For instance, try the following command:

# less -M filename

# less -M filename

You should note that less might take a moment to calculate these statistics for very long files. You can interrupt this process with Ctrl + C.

When using less with piped input, the = key will only display limited information, as the full scope of the file (like total lines and bytes) won’t be known until the end is reached.

Also Read: 6 Simple Examples of Using the Linux watch Command

Also Read: The Linux bc Command with 9 Practical Examples

Conclusion

The less command is key for handling text files efficiently in Linux. It’s really helpful for tasks like opening and looking at files, keeping an eye on log updates as they happen, and doing detailed searches.

Moreover, the integration of less with other Linux commands makes it indispensable for Linux tasks. The ability to seamlessly navigate through files, search for specific content, and even monitor real-time data changes, positions less as a powerful utility for everyday tasks.

RedSwitches offers the best dedicated server pricing and delivers instant dedicated servers, usually on the same day the order gets approved. Whether you need a dedicated server, a traffic-friendly 10Gbps dedicated server, or a powerful bare metal server, we are your trusted hosting partner.

FAQs

Q. What is the less command in Linux?

The less command in Linux is a terminal pager program used to view the contents of a text file one screen at a time. Unlike the more command, less allows backward navigation in the file and forward navigation.

Q. How do I open a file using less?

To open a file in less, simply type less [filename] in the terminal. Replace [filename] with the actual name of the file you want to view.

Q. Can I search for text within a file using less?

Yes, you can. While viewing a file in less, type /[search text] and press Enter to search downwards. To search upwards, use ?[search text].

Q. How do I navigate through a file in less?

Use the arrow keys to move line by line, or Page Up and Page Down to move by full screens. You can also use the spacebar to scroll forward and b to scroll backward.

Q. Is it possible to open multiple files with less?

Yes, you can open multiple files by typing less file1 file2 …. Navigate between files using :n for the next file and :p for the previous file.

Q. How do I exit the less command?

Press q to quit less and return to the command prompt.

Q. Can less display line numbers?

To display line numbers in less, open a file with less -N [filename] or type -N while viewing a file in less.

Q. How do I view a specific part of a file in less?

You can directly jump to a specific line by typing [line number]G in less. For example, 50G would take you to the 50th line.

Q. Is it possible to customize the behavior of less?

Yes, you can customize less by setting options in the Less environment variable. For example, export LESS=’-N -M’ sets default options to display line numbers and detailed status lines.

Q. Can less handle binary files?

While less is primarily designed for text files, it can open binary files safely. However, the display may not be meaningful as less interprets the data as text.

Try this guide with our instant dedicated server for as low as 40 Euros

Deploy Now
SHARE
Back to blog
Check Out Pre-Configured Bare-Metal Servers
View Stock
CUSTOM SOLUTIONS
Instant dedicated server
Dedicated Server
Managed Dedicated Server
Bare Metal Server
Dedicated Server with Bitcoin
10Gbps Dedicated Server
Crypto Hosting
Storage Dedicated Server
High Availability Cluster
Video & IPTV Streaming
CDN & VPN Hosting
Ad-Tech & Mar-Tech Hosting
Server Locations
SUPPORT TOOLS
Affiliate Program
Client Area
Support Ticket
LEGAL
Service Agreement
Terms Of Service
Acceptable Use Policy
Privacy Policy
Logo
RedSwitches Is a global hosting provider offering Dedicated Servers, Infrastructure As a Service, Managed Solutions & Smart Servers in 20 global locations with the latest hardware and premium networks.
20 Collyer Quay, #09-01, Singapore 049319
sales@redswitches.com
NETWORK
BLOG
CONTACT US
WHY REDSWITCHES?
Follow us on
Path  Path (1)   Instagram
2024 RedSwitches Pte. Ltd. All Rights Reserved.
Made With ♥ In Singapore
Payment Logos
