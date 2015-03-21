from the [observations file][examples/Ch3observations.txt] 

13 January, 1752 at 13:53	-1.414	 5.781	 Found in tide pools
17 March, 1961 at 03:46	 14	 3.6	 Thirty specimens observed
1 Oct., 2002 at 18:22	 36.51	 -3.4221	 Genome sequenced to confirm
20 July, 1863 at 12:02	 1.74	 133	 Article in Harper's

Look at the data you have, describe it, and describe what you want the end up with, here we want:

Year	Mon.	Day	Hour	Minute	Xdata	Ydata

Separate the data you have based on this desire:

13 	January,	1752	at 	13:53	-1.414 	5.781 	Found in tidepool

Put parenthesis around the parts you want to keep and assign numbers to those parenthesis

(13) 	(Jan)uary,	(1752)	at 	(13):(53)	-(1.414) 	(5.781) 	etc.
 1        2           3          4    5         6          7

 Now put regex expressions in for each section - I still don't understand the []
 it looks like in group two below, the [\w\,\.]* means there could be a period or a comma or both.

(13) 	(Jan)uary,			(1752)	at 	(13):(53)	-(1.414) 	(5.781) 	etc.
(\d+)	(\w\w\w)[\w\,\.]*	(\d+)    at (\d+):(\d+) ([-\d\.]+)  ([-\d\.]+)	.*
 1        2          		  3          4    5         6          7 

Go back through the search string and add spaces (one or more), we also replaced the \w\w\w with \w{3} - which means the same thing.

(13) 	(Jan)uary,			(1752)	at 	(13):(53)	-(1.414) 	(5.781) 	etc.
(\d+)\s+(\w{3})[\w\,\.]*\s+(\d+)\sat\s(\d+):(\d+)\s+([-\d\.]+)\s+([-\d\.]+).*
 1        2          		  3          4    5         6          7 

 Check your search string in the text editor using find - make sure regex is turned on

 Now name the replacement fields
 Day	Mon	Year	Hour	Minute Xdata 	Y
  1      2   3       4        5      6       7

  Now look back at what we want:

Year	Mon.	Day	Hour	Minute	Xdata	Ydata
 \3     \2\.    \1   \4      \5      \6       \7

\3\t\2\.\t\1\t\4\t\5\t\6\t\7

Which gives us:

1752	Jan.	13	13	53	-1.414	5.781
1961	Mar.	17	03	46	14	3.6
2002	Oct.	1	18	22	36.51	-3.4221
1863	Jul.	20	12	02	1.74	133

Beautiful.






