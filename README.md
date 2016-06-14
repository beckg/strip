<b>strip - a stripboard layout tool</b>

I use veroboard for many of my projects, which in the past has led to either very unsightly boards
or lots of pencil drawings as I work out how to route the signals.
<br><br>
I periodically look for software to alleviate these problems but have failed to find anything that made 
the task any easier or that I was prepared to pay for. I did find 
<a href="https://sites.google.com/site/libby8dev/stripes">Stripes</a>
and liked much of what I saw, but found some problems with the implementation.
Therefore I took some of the ideas and developed an alternative solution. I know that one should resist 
not-invented-here, but sometimes it is fun to play!  The philosophy of using Java so 
that you have a cross platform solution is important. 
<br><br>
You will need an installed version of Java 6, 7 or 8. 
<a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html">Java</a>
<br><br>
You will need to clone this repository and the common repository. The make(nmake) files show the trivial build.
<br><br>
The makefile contains a run target 'run', otherwise the following command should work on linux.
<pre><b>$(JAVA_HOME)/bin/java -classpath jar/strip.jar org.aventinus.strip.Strip</b></pre>
and the following on windows.
<pre><b>java -classpath .\jar\strip.jar org.aventinus.strip.Strip</b></pre>
You should see a default board:
<br><br>
<img src=https://raw.github.com/beckg/resources/master/strip/emptyStrip.gif height="298"/>
<br><br>
A quick look around the menus will give you a feel for the kinds of things that you can do - nothing suprising.
BoardProperties allows you to change the number of rows and the number of holes. There is a "bench" that
can surround the strip where you can drop unplaced components - it was an idea that did not really gel.
<br><br>
A layout is saved in a modified version of the 
<a href="https://raw.github.com/beckg/common/master/json.md">JSON</a>
format.
<br><br>
The important action is "right-click" over the strip.
<br><br>
<img src=https://raw.github.com/beckg/resources/master/strip/stripMenu.gif alt="layout"/>
<br><br>
Place a component. If you "left-click" over the body of the component, then you can drag the whole component; if you
"left-click" over a connector (wire-through-hole), then (usually) you can drag just the connector. Some components, 
such as IC pads, only move as a whole.
<br><br>
If you "right-click" over a component, then the menu contains aditional options. 
<br><br>
<img src=https://raw.github.com/beckg/resources/master/strip/stripEdit.gif alt="layout"/>
<br><br>
The edit option allows you to change any options - for example the size of that electrolytic. It is worth checking 
the edit dialogue for each kind of component. It also allows you to record a name, value, and some 
details about the purpose of the component - a bit of documentation. The name is important. 
<br><br>
Add a wire and a couple of spot-cuts, set the "Tools->Test" option in the menu and "left-click" one end of the wire.
<br><br>
<img src=https://raw.github.com/beckg/resources/master/strip/testStrip.gif alt="layout"/>
<br><br>
Clear the board - "left-click" above and left of all the components and drag below and right and press delete.
Add an electrolytic E1, add a resistor R1.
<br><br>
<img src=https://raw.github.com/beckg/resources/master/strip/e1Tooltip.gif alt="layout"/>
<img src=https://raw.github.com/beckg/resources/master/strip/r1Tooltip.gif alt="layout"/>
<br>
Create a file containing...
<pre>R1 0 1
E1 0 1</pre>
... save it as test.net - or some such. File->Compare NetList, navigate to and select the file. You should get a 
window that says...
<pre>Start compare ... 
... end compare</pre>
The netlist in the file has been checked against the netlist implied by the layout and found to represent the 
same circuit.
<br><br>
If there are differences then these will be listed. The output can be hard to understand - more work is needed
here. A single mis-wiring can lead to a cascade of errors. Build up the circuit slowly, missing components 
seem to be easier to work with that incorrectly wired ones. The actual checking seems to be correct; the errors
are real! The program will try and correct pin ordering for "reversible" components - resistors and non-electrolytics.
<br><br>
As a last resort you can use File->Export NetList. However, you have to be very careful. When you check the 
netlist against your designs it is easy to confuse the orientation of components such as 3-terminal ICs and
convince yourself that the netlist represents your drawing.
<br>
The printing basically works. It is a little rough around the edges - titles and some scaling. It prints two versions
of the naked board one from each side.



