COVER ART
https://archive.org/details/pradoadescripti01gallgoog/page/n298/mode/2up?q=devouring


THE EMPTY HOUSE AND OTHER GHOST STORIES
(1906)
https://www.gutenberg.org/files/14471/14471-h/14471-h.htm
https://archive.org/details/emptyhouseotherg00blacrich/mode/2up
Produced by Michael Ciesielski, Annika Feilbach
THE EMPTY HOUSE                                             [Done]
A HAUNTED ISLAND                                            [Done]
A CASE OF EAVESDROPPING                                     [Done]
KEEPING HIS PROMISE                                         [Done]
WITH INTENT TO STEAL                                        [Done]
THE WOOD OF THE DEAD                                        [Done]
SMITH: AN EPISODE IN A LODGING-HOUSE                        [Done]
A SUSPICIOUS GIFT                                           [Done]
THE STRANGE ADVENTURES OF A PRIVATE SECRETARY IN NEW YORK   [Done]
SKELETON LAKE: AN EPISODE IN CAMP                           [Done]

The Willows (1907)
https://www.gutenberg.org/cache/epub/11438
https://archive.org/details/TheWillows/page/n35/mode/2up
Produced by Suzanne Shell, David Newman and PG Distributed Proofreaders

The Wendigo (1910)
https://www.gutenberg.org/ebooks/10897
https://archive.org/details/TheWendigo
Suzanne Shell, Beginners Projects, Dave Morgan and the


Day and Night Stories (1917)
https://www.gutenberg.org/ebooks/45964
https://archive.org/details/dayandnightstori00blacrich                                                                                                                                                                                                                                                                                                                                                                                                          
Produced by "None Named"
    The Tryst                       [Done]
    The Touch of Pan    		    [Done]
    The Wings of Horus (1914)       [Done]
    Initiation  (1916)    		    [Done]
    A Desert Episode  (1914)        [Done]
    The Other Wing (1915)    	    [Done]
    The Occupant of the Room (1909)	[Done]
    Cain’s Atonement (1915)    	    [Done]
    An Egyptian Hornet (1915)       [Done]
    By Water (1914)    		        [Done]
    H. S. H.  (1913)    		    [Done]
    A Bit of Wood (1914)    	    [Done]
    A Victim of Higher Space  (1914)  [Done]
    Transition (1913)    		    [Done]	
    The Tradition (1913)    	    [Done]

The Wolves of God (1921)
https://www.gutenberg.org/ebooks/38310
https://archive.org/details/wolvesgodandoth01wilsgoog
Produced by David Starner, eagkw 
    The Wolves of God (1921)    	    [Done][Not Read]
    Chinese Magic (1920)    	        [Done][Not Read]
    Running Wolf (1920)    	            [Done][Not Read]
    First Hate (1920)    	            [Done][Not Read]
    The Tarn of Sacrifice (1921)        [Done][Not Read]
    The Valley of the Beasts (1921)    	[Done][Not Read]
    The Call (1919)    	                [Done][Not Read]
    Egyptian Sorcery (1921)    	        [Done][Not Read]
    The Decoy (1919)    	            [Done][Not Read]
    The Man Who Found Out (1912)    	[Done][Not Read]
    The Empty Sleeve (1911)    	        [Done][Not Read]
    Wireless Confusion (1919)    	    [Done][Not Read]
    Confession (1921)                   [Done][Not Read]
    The Lane that ran East and West (1921) [Done][Not Read]
    “Vengeance is Mine” (1921)          [Done][Not Read]


The Olive (1922)
https://www.gutenberg.org/ebooks/9363
https://archive.org/details/bestbritishshor00unkngoog/mode/2up
Etext produced by Stan Goodman, Tonya Allen


FOUR WEIRD TALES
http://www.gutenberg.org/files/16726/16726-h/16726-h.htm
Produced by Suzanne Shell, Geetu Melwani 
The Insanity of Jones (1907)     (From The Listener and Other Stories)
The Man Who Found Out            [ALREADY HAVE THIS]
The Glamour of the Snow (1911)   (From Pan's Garden)
Sand (1912)                      (From Pan's Garden)



=================


Doing this down to the point of the multiple regex searches, then stopping. 


RECHECK PUB YEARS EVERYWHERE

++++++++++++++


se create-draft --author="Algernon Blackwood" --title="Short Fiction" --pg-url="https://www.gutenberg.org/ebooks/11438"
cd algernon-blackwood_short-fiction


wget -O src/epub/text/body.xhtml "http://www.gutenberg.org/files/16726/16726-h/16726-h.htm"
file -bi src/epub/text/body.xhtml
iconv --from-code="ISO-8859-1" --to-code="UTF-8" < src/epub/text/body.xhtml > src/epub/text/tmpmv src/epub/text/tmp src/epub/text/body.xhtml
perl -pi -e "s|<h2|<\!--se:split--><h2|g" src/epub/text/body.xhtml
se split-file src/epub/text/body.xhtml 
mv chapter* src/epub/text/
rm src/epub/text/body.xhtml
se clean .
se typogrify .
sed --regexp-extended --in-place "s|([0-9])+’|\1′|g" src/epub/text/*
sed --regexp-extended --in-place "s|([0-9])+”|\1″|g" src/epub/text/*

[a-zA-Z]\.?\s*&\s*[a-zA-Z]
(?<!en-)(?<!z3998:roman">)(?<![A-Z])[A-Z]{2,}(?!")
—[’”][^<\s]
[’”][,.]


se semanticate .
git difftool

sed --regexp-extended --in-place "s|[A-Z’]{2,}|<em>\L&</em>|g" src/epub/text/*
sed --regexp-extended --in-place "s|en-<em>([a-z]+)</em>|en-\U\1|g" src/epub/text/*

se modernize-spelling .

git remote add origin https://github.com/kingrpaul/algernon-blackwood_short-fiction.git

###########################


se build-images .

se print-manifest --in-place .
se print-spine --in-place .
se print-toc --in-place .
se build --output-dir=$HOME/dist/ --kindle --kobo --check .

