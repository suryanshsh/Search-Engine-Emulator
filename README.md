# Search-Engine-Emulator
Simple Python Search Spider, Page Ranker, and Visualizer

This is a set of programs that emulate some of the functions of a 
search engine.  They store their data in a SQLITE3 database named
'spider.sqlite'.  This file can be removed at any time to restart the
process.   

You should install the SQLite browser to view and modify 
the databases from:

http://sqlitebrowser.org/

This program crawls a web site and pulls a series of pages into the
database, recording the links between pages.

Note: Windows has difficulty in displaying UTF-8 characters
in the console so for each console window you open, you may need
to type the following command before running this code:

    chcp 65001

http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how

Enter web url or enter: http://www.dr-chuck.com/
['http://www.dr-chuck.com']
How many pages:2
1 http://www.dr-chuck.com/ 12
2 http://www.dr-chuck.com/csev-blog/ 57
How many pages:

In this sample run, we told it to crawl a website and retrieve two 
pages.  If you restart the program again and tell it to crawl more
pages, it will not re-crawl any pages already in the database.  Upon 
restart it goes to a random non-crawled page and starts there.  So 
each successive run of spider.py is additive.



You can have multiple starting points in the same database - 
within the program these are called "webs".   The spider
chooses randomly amongst all non-visited links across all
the webs.

If you want to dump the contents of the spider.sqlite file, you can 
run spdump.py as follows:

Mac: python3 spdump.py 
Win: spdump.py

(5, None, 1.0, 3, u'http://www.dr-chuck.com/csev-blog')
(3, None, 1.0, 4, u'http://www.dr-chuck.com/dr-chuck/resume/speaking.htm')
(1, None, 1.0, 2, u'http://www.dr-chuck.com/csev-blog/')
(1, None, 1.0, 5, u'http://www.dr-chuck.com/dr-chuck/resume/index.htm')
4 rows.

This shows the number of incoming links, the old page rank, the new page
rank, the id of the page, and the url of the page.  The spdump.py program
only shows pages that have at least one incoming link to them.

Once you have a few pages in the database, you can run Page Rank on the
pages using the sprank.py program.  You simply tell it how many Page
Rank iterations to run.



You can dump the database again to see that page rank has been updated:



You can run sprank.py as many times as you like and it will simply refine
the page rank the more times you run it.  You can even run sprank.py a few times
and then go spider a few more pages sith spider.py and then run sprank.py
to converge the page ranks.

If you want to restart the Page Rank calculations without re-spidering the 
web pages, you can use spreset.py

All pages set to a rank of 1.0


For each iteration of the page rank algorithm it prints the average
change per page of the page rank.   The network initially is quite 
unbalanced and so the individual page ranks are changing wildly.
But in a few short iterations, the page rank converges.  You 
should run prank.py long enough that the page ranks converge.

If you want to visualize the current top pages in terms of page rank,
run spjson.py to write the pages out in JSON format to be viewed in a
web browser.

Mac: python3 spjson.py 
Win: spjson.py 

Creating JSON output on spider.js...
How many nodes? 30
Open force.html in a browser to view the visualization

You can view this data by opening the file force.html in your web browser.  
This shows an automatic layout of the nodes and links.  You can click and 
drag any node and you can also double click on a node to find the URL
that is represented by the node.

This visualization is provided using the force layout from:

http://mbostock.github.com/d3/

If you rerun the other utilities and then re-run spjson.py - you merely
have to press refresh in the browser to get the new data from spider.js.

