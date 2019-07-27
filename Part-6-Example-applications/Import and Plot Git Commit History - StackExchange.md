This package provides couple of functions for plotting commits data from GiHub:

    Import["https://raw.githubusercontent.com/antononcube/MathematicaForPrediction/master/Misc/GitHubPlots.m"]

    GitHubDateListPlot["hadley", "plyr"] 

[![enter image description here][1]][1]

    GitHubBarChart["hadley", "plyr"]

[![enter image description here][2]][2]

I think these plots are similar enough to the image in the question. There are number of questions to be answered in order to program them. For me the most important one is how to get the data, which was answered by [Pickett][3] in a comment.

The commit messages on the plot ticks are click-able -- they link to the corresponding commits in github.com. Both `GitHubDateListPlot` and `GitHubBarChart` take options that can be given to the corresponding functions `DateListPlot` and `BarChart`.

For example, we can focus on an area of interest (PlotRange) and/or change the image size (ImageSize):

    GitHubDateListPlot["hadley", "plyr", 
     PlotRange -> {{{2015, 04, 01}, {2015, 04, 20}}, {0, 26}}, 
     ImageSize -> {Automatic, 600}]

[![enter image description here][4]][4]

Also, the points on the plots made by `GitHubDateListPlot` have tooltips and the commit nodes of a path are highlighted with mouse-over. (This can be seen in the plots above.)

Some details follow.

1. Getting the data.
   GitHub provides a web service API. See the comment by Pickett above.

2. Combining text characterizing the commits with graphics of the commits dependencies.
   One way to do this is to use functions like `DateListPlot` and `BarChart` as a base. The plots` frame ticks are with (some) commit data, and their graphic elements are for the commit dependencies.

3. Parsing the commits data.
   This can be done with an ad-hoc parser. This parser has to be modified if GitHub changes the format of the returned results.

4. Dependencies layout. This is nice to have and here is a quick but not really good approach.
   A graph of the commits dependencies is made.
   The roots and the leaves are identified.
   The paths from all roots to all leaves are found.
   The paths a plotted starting with the longests first. In this way the shortest path (e.g. the trunk)
   is going to be most visible, which intuitively makes sense.
   This is not the best approach. The paths are most likely to be many and the layout gets cluttered.
   Note that the function `GitHubDateListPlot` uses `RandomSample` for the color of dependency lines.

There are several options that would be nice to be added to the functions in the package, like, font size of the ticks, coloring, line thickness, login credentials (if applicable), etc. A dedicated error handling is probably a must. 

Also, there are probably bugs in the code -- I have tested it only with 4-5 repositories.

Here is an example with [halirutan][5]'s "Mathematica-IntelliJ-Plugin" project (which I used to write the package):

[![enter image description here][6]][6]

At this point, of course, we can just import and plot a bunch of GitHub repositories:

    ghDLPlots = 
      Map[GitHubDateListPlot["hadley", #, 
         PlotLabel -> Style[#, "Subsubtitle"], 
         FrameTicks -> {{All, All}, {Automatic, Automatic}}, 
         AspectRatio -> 4] &, {"plyr", "ggplot2", "devtools", "dplyr", 
        "adv-r", "rvest"}];
    Grid[{ghDLPlots}]

[![enter image description here][7]][7]


**Update**

I made a package with an object-oriented implementation of the discussed above ingestion and visualization tasks for GitHub commits data.

    Import["https://raw.githubusercontent.com/antononcube/MathematicaForPrediction/master/Misc/GitHubDataObjects.m"]

The implementation uses the design patterns Template Method, Strategy, Decorator, and Composite described in the
book:

> [GoF-94] Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides,
>            [Design Patterns: Elements of Reusable Object-Oriented Software][8], Addison-Wesley, 1994.

The implementation is a modified and extended version of the functions in the package ["GitHubPlots.m"][9] (demonstrated above.)

The most significant feature of this package is the method "Plot3D" for a collection of GitHub projects (using the [design pattern][8] [Composite][10]). Here is an example how to use it:

    ghs = Map[MakeGitHubDataObject["hadley", #] &, {"plyr", "dplyr", "adv-r", "ggplot2", "devtools", "rvest"}]
    ghComposite = GitHubDataComposite[Unique[], ghs]
    ghComposite[
     "Plot3D"["ProjectPlanes" -> True, "GlobalTimeOrder" -> False, 
      BoxRatios -> {1, 2, 2}, ImageSize -> {Automatic, 1000}]]

[![enter image description here][11]][11]

The method "Plot3D" can take the option "SubsetQueryFunction"->`selectFunc` that allows for selection of points that adhere to a predicate. The function `selectFunc` is used in the Dataset's object corresponding to the projects and from the obtained rows the subset of points is derived. 

The query points are shown in purple in the plot below. Also the plot uses global order in time of the commit points on the z-axis. (The previous plot used local, per project commit order.)

    ghComposite[
     "Plot3D"["ProjectPlanes" -> False, "GlobalTimeOrder" -> True, 
      "SubsetQueryFunction" -> (StringMatchQ[#committer, ___ ~~ 
           "Hadley" | "hadley" ~~ ___] &), "SubsetLines" -> True, 
      "SubsetPlotStyle" -> {PointSize[0.02], Lighter[Purple], 
        Arrowheads[10^-7.7, Appearance -> "Flat"]}, 
      PlotLabel -> "Hadley Wickham", BoxRatios -> {1, 2, 2}, 
      ImageSize -> {Automatic, 1000}]]

[![enter image description here][12]][12]


  [1]: http://i.stack.imgur.com/Gn02i.png
  [2]: http://i.stack.imgur.com/tcoMn.png
  [3]: http://mathematica.stackexchange.com/users/731/pickett
  [4]: http://i.stack.imgur.com/L2a1y.png
  [5]: http://mathematica.stackexchange.com/users/187/halirutan
  [6]: http://i.stack.imgur.com/4eKtF.png
  [7]: http://i.stack.imgur.com/6iS6u.png
  [8]: https://en.wikipedia.org/wiki/Design_Patterns
  [9]: https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/GitHubPlots.m
  [10]: https://en.wikipedia.org/wiki/Composite_pattern
  [11]: http://i.stack.imgur.com/AFH92.png
  [12]: http://i.stack.imgur.com/cBxgx.png
