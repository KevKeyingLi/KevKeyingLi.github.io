# Visualization Fundamentals
### A few examples of Visualization
* THe cover of book: http://www.vizwiz.com/2013/01/alberto-cairo-three-steps-to-become.html
* https://www.youtube.com/watch?v=jbkSRLYSojo 
* Healthcare spending and life expectancy from OECD Health Data 2009
* https://d17h27t6h515a5.cloudfront.net/topher/2016/September/57e9a59d_l1-worldcuptopscorers/l1-worldcuptopscorers.png
* 

## Over view
### What is good data visualizaiton?
Generally two purposes of data visualization:
* Exploratory
    * enable the user to explore the data, connect things in interesting ways, and look at data from different angles in an unbiased and unleading way.
* Explanatory
    * A robust understanding of the context
        * who your audience is, what they need to know or do
    * Choosing an appropriate type of visual. what kind of graph and visualization allow them to do that in the most easy and straightforward fashion.
    * Clutter, getting comfortable identifying eliminating those things that aren't informative. Decrease cognitive load and causes our data to stand out 
    * Draw your audiences attention to where you want them to pay: color, size, placement
    * Around story, story telling: 
        - An amazing story: The cover page of "The functional art"

### What is the essential background for create good data visualization.(from Zipfian Academy)
* Your greatest insight is at most as good as your communication
* Art+Science. Designer+Engineer+Storyteller

### Data Visualization in Data Science process
The process: 
* acquire -> parse/wrangling(most time consuming part) : **Computer Science** ETL
* filter -> mine: Exploratory data analysis(EDA), **Statistics and Data Mining** model the data
* represent -> refine: Graphic Design(DV)
* interact: Info-vis and HCI(DV)

For this course: 
* L1 and L2 focus on represent and refine, graphic design
* L3 and L4 focus on the interact with data, infovis and HCI

The process of data science and data visualization is a process of iteration. 
### Exploratory importance
Anscombe’s Quartet

matplotlib in python, ggplot in R


### Different kinds of data types:
* Quantative data: continuous, discrete
* Categorical data: Nominal data
* Ordered data, e.g. a few ranges that can be ordered. 

### Visual Encodings
data -> visualization features. 

* Planar Variables:
    - Position(x,y)
* Retinal Variables like:
    - size, particularly good for ordered data. 
    - orientation(ordered data)
    - color saturation(ordered data)
    - color hue(nominal)
    - shape(nominal)
    - texture(nominal)
* Animation
    - time 

Examples:
World Cup Top Scores: https://d17h27t6h515a5.cloudfront.net/topher/2016/September/57e9a59d_l1-worldcuptopscorers/l1-worldcuptopscorers.png

Lose or Draw: https://d17h27t6h515a5.cloudfront.net/topher/2016/September/57e9a683_l1-winloseordraw/l1-winloseordraw.png

An article on visual encoding
https://www.targetprocess.com/articles/visual-encoding/

### Rankings of Visual Encodings

A 1985 paper on this topic of what encodings are most effective
https://web.cs.dal.ca/~sbrooks/csci4166-6406/seminars/readings/Cleveland_GraphicalPerception_Science85.pdf

Nathan's Yau summarizes the findings of the paper and provides sound advice for putting it into practice on his blog, Flowing Data.

Basically, Position, length are more accurate, Density and Hue are less accurate. 

When we design a visualization we want to know what is the most important information that we want to get through, and use the most accurate encoding for that. 


# D3 building blocks











