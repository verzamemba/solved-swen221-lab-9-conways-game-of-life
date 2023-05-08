Download Link: https://assignmentchef.com/product/solved-swen221-lab-9-conways-game-of-life
<br>
In this lab you will revisit the implementation of Conway’s <em>Game of Life </em>seen in an earlier lab. The purpose of this lab is consider the implementation of that program using Java 8 <em>lambda expressions</em>, rather than using <em>inheritance</em>. You will find that the implementation using lambda’s is more concise and simpler to write.

<h1>Conway’s Game of Life</h1>

Recall that Conway’s <em>Game of Life </em>is a simple cellular simulation devised by John Horton Conway (a British mathematician) in 1970. The Game of Life has been studied extensively since then for both scientific interest, and also just for fun. For example, it has been shown that the problem of deciding whether a given state of the game will ever reach the empty board is <em>undecidable</em>. A simple example is:

Here, cell’s marked in black are “alive” whilst those in white are “dead”. Conway identified four rules for governing the transition between life and death in the Game of Life:

<ol>

 <li>Any live cell with fewer than two live neighbours dies, as if caused by <em>under-population</em>.</li>

 <li>Any live cell with exactly two live neighbours continues on to the <em>next generation</em>.</li>

 <li>Any live cell with more than three live neighbours dies, as if by <em>over-population</em>.</li>

 <li>Any dead cell with exactly three live neighbours becomes a live cell, as if by <em>reproduction</em>.</li>

</ol>

Here, the neighbours of a cell are the <em>eight </em>surrounding cells (i.e. the four cells at <em>North</em>, <em>South</em>, <em>East</em>, and <em>West </em>and the four diagonals at <em>NorthWest</em>, <em>NorthEast</em>, etc). See en.wikipedia.org/wiki/Conway’s_ Game_of_Life for more.

In this lab, we are going to play with an extensible implementation of the Game of Life. The implementation is extensible because new rules can easily be written to control the game in different ways. The implementation also supports more complex forms of the Game, as it allows for more than just cells which are “alive” or “dead”. Instead, each cell is in a state between 0 and 9, where 9 corresponds roughly to “dead” and the other states to varying forms of “alive”. The meaning of the intermediate states is left up to the rule implementor, but can be used to simulate <em>age</em>, <em>sickness</em>, <em>happiness</em>, etc.

<h1>Getting Started</h1>

To get started, download the lambda-conway.jar file from the course website and import this into an Eclipse project. The Game of Life is provided with a Graphical User Interface, which you can run by rightclicking on GameOfLife and selecting “Run As−→Java Application” (ignore CellDecayGameOfLife for now). You should see a window pop up like this:

You can play the game by clicking on the window to place cells and the starting the simulation by pressing “run”. Take a few minutes to play around with the game. You should notice that not all rules are implemented and we will begin by fixing them in Activity 1.

NOTE: it is useful to take the time and revisit the implementation of Conway using inheritance from an earlier lab. You will notice that the rules package is no longer required in the implementation for this lab. <em>In fact, the number of classes required has reduced by four in total</em>.

<h1>Activity 1: Conway’s Missing Rules</h1>

The implementation of the Game of Life provided does not properly implement rules (3) and (4) from above. The goal of this activity is to complete these rules. The rules themselves are implemented using lambda expressions. For example, Conway’s <em>underpopulation </em>rule is implemented as follows:

<table width="662">

 <tbody>

  <tr>

   <td width="662"><strong>public static final </strong>Rule[] ConwaysOriginalRules = {<em>/ /         The underproduction           rule</em>(Pair&lt;Point,Board&gt; p) -&gt; neighbours(p) &lt; 2 ? DEAD : <strong>null</strong>, …};</td>

  </tr>

 </tbody>

</table>

1

2

3

4

5

This implementation of the rule is very easy to compare with the original English description. You will find this rule in the class GameOfLife and it should provide a useful guide which you can follow. Having completed rules (3) and (4), you should find that all tests in GameOfLifeTests now pass.

<h1>Activity 2: Cell Decay</h1>

The goal now is to implement a variation on the basic rules for the Game Of Life which models the age of a cell. Our updated rules for the game are:

<ol>

 <li>Any live cell with fewer than two live neighbours gets <em>older</em>, as if caused by <em>under-population</em>.</li>

 <li>Any live cell with two live neighbours continues <em>in stasis </em>to the <em>next generation</em>.</li>

 <li>Any live cell with more than three live neighbours gets <em>older</em>, as if by <em>over-population</em>.</li>

 <li>Any cell with exactly three live neighbours gets <em>younger</em>, as if by <em>happiness</em>.</li>

</ol>

The age of a cell is determined by its current state which, if you recall, is a value between 0<em>…</em>9. Here, 0 is youngest whilst 9 is oldest. We consider that cells of age 9 are <em>dead</em>, whilst all others are varying forms of <em>alive</em>. At this point, we will now concentrate on using the variation CellDecayGameOfLife and the accompanying test cases, CellDecayTests. You can run the simulation as a Java Application with CellDecayGameOfLife, though at this stage you should find that it does <em>nothing</em>.

What to do. Your aim is to implement the above rules for cell decay. You should add any rules you create to the CellDecayRules array in CellDecayGameOfLife, as was done for the original GameOfLife. Having done this, all tests in CellDecayTests should now pass.

Having completed this part, you should find that the balance has tipped and cell growth expands <em>quickly</em>. This is because cells stay “alive” for much longer than before. For example, the system will often produce something like this: