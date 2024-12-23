java c
CS152
Project 8:   Pinball Wizard
The focus of this   project   is to continue reworking our classes   into   an   inheritance   hierarchy   and   adding   new shapes to our visualization. We will also use a   dictionary   to   make working   with collisions more streamlined.
Project Tasks
T1. Create a   Block   class
The first task   is to create a Block   child class   using   inheritance. The   parent   class   is   Thing).
a.       Define the   Block                init               method
The                init            method should have the following   signature. You   are   welcome   to   add   additional   optional arguments.
def          init         (self, win,x0=0,y0=0,width=2,height=1, color=None):
As with the   Ball class, the first action   in the                init               method   is   to   call   the   parent
Thing.            init            method. Specify   the type as the string "block". Any   parameters you   don't   pass to the   Thing.            init            method should then   be assigned   to   their   proper field.
Assign the dx   parameter to the field self.dx and the dy   parameter to   the field   dy.   You   can   use   self.width and self.height if you wish (or any other   names   of your choice).
Finally, call self.reshape() and self.color() to set   up the vis   list   and   set   the   color.
b.       Create the   reshape method
def   reshape   (self):
The   reshape   method should undraw the graphics objects if they   are   drawn.   Then   it   should   define the self.vis   list of graphics objects using   the   current   fields.   Then   it   should   draw   the   graphics objects   if they are drawn.   Note that   if you use the undraw   and   draw   methods,   they      affect the value of self.drawn. Therefore,   it's best to make   a   local   copy   of self.drawn   and   use   that to test   if the object   needs to be   undrawn/drawn.
When creating the visualization for the   Block,   put the anchor point   in the   center of the   block.   One corner should be at (x0-width/2, y0-height/2)   and   the   other   corner   should   be   at (x0+width/2, y0+height/2).
c.       Write getWidth and   getHeight
These two functions should return the width or   height of the   block.
d.      Write setWidth and setHeight
These two functions should update the value of the width (dx)   field   or the   height   (dy)   field   and then call the   reshape   method.
T2.   Make another shape class of your choice
Choose a shape.   It can   be a   polygon (e.g.   a triangle   or   a   pentagon)   or   it   could   be   a   multi-object shape like a snowman. The new   shape   class   should   inherit from   Thing.   The                     init            method   should   make sure all the   necessary   information   is   provided and finish by calling   reshape   and   setColor.
The   reshape method should define the graphics objects   that   define   the   simulated   object.   It's         ok if this class is just a single graphics object.   When   you   define   the   object's   visualization,   define   it so that the object's position corresponds to   the   center   of the   object, just like   it   did   for   the   Ball         and   Block classes.
If the shape   is   best   modeled as a   block (for the   purpose of collisions) then   it will   need   getHeight, getWidth, setHeight,   and   setWidth   methods.   If the shape   is   best modeled as a circle, then it will   need   getRadius   and   setRadius   methods.If the class   has a complicated color scheme, you may   need   to   write   a   setColor   for   the   child   class.   If the class   is a   multi-shape object, you   may   need to write a set   Position function for   the   child class.
T3. Write a   unified collision function
The   next task   is to   modify the   collision.py   file to   make   it simpler to call the right   collision function no matter what types of objects are   involved.   (Note, the   collision functions   all work with   a ball and something else. We don't yet   have   block-block   collisions, for   example.)The   idea   is to   use a dictionary with the two types   involved   in the collision   as   the   key,   making   use of the type field   in the Thing class.   For example,   if we   have two objects,   item1   and   item2,   we can create   a   key   by writing:
key =   (item1.getType   (),   item2.getType   ())
The   key   is a tuple that   has two strings   in   it. Then, we can   generate   a   dictionary   entry   that   contains all the   possible   keys and stores the   proper function to call   in each   case.   For   example,   the following creates an   entry in the dictionary   collision_router with   the   key   ('ball',   'ball')   and   sets its value to the function reference   collision_ball_ball.
collision_router   [   ('ball',   'ball')   ] = collision_ball_ball
The above line creates a new   entry   in   the   collision_router   dictionary with   the   key   ('ball',   'ball')   and   its value   is a function reference to the collision_ball_ball function   (note there   are   no   parentheses after collision_ball_ball). This entry in the dictionary   can   be   used   to   call   the   collision_ball_ball function using the following syntax.
collision_router   [   (   'ball   ',   'ball   ')   ]   (thing1, thing2)
At the bottom of the   collision.py   file, at the top level   (meaning   totally   unindented),   create   an empty dictionary called   collision_router. Then add an entry to   the   dictionary   (as   above) for each   possible collision of a ball and   another type:   ball,   block,   and the   additional   shape you created (which should be treated   as   either   a   ball   or   a   block.
Finally, create a function called   collision   (ball, thing,timestep)that takes   in   two   Thing objects   plus a time step and uses the   collision_router   dictionary   to   call   the   right   function.   Assume that the   ball   is always the first   parameter and the other object   (ball,   block, or   other)   is      the second   parameter.
T4. Create an animated scene with   obstacles
Required   Element   1:   pinball.py
Create a   new file   name   pinball.py   In this file you will create a scene   that   is   like   a   pinball   table.   If   you don’t   know what that   is follow this link: Pinball   Machine
Your pinball   machine should   have outside boundaries   made of   rows   of   blocks   and   some obstacles   inside the   box that are all stationary.   It does   not   need to   be   completely   enclosed.
The default   behavior. should   be for the   program to launch a single   ball   into   the   scene   and   have   it   bounce around.
To create the scene, the following is a   suggested   structure for your   code   to   get   started.
def buildObstacles   (win):
# Create all of   the   obstacles   in   the   scene   and put   them
in   a   list
# Each obstacle should be   a   Thing   (e.g.   Ball,   Block,
other)
# You might want to give   one   or more   the   obstacles   an
elasticity >   1
# Return the   list   of   Things
def main   ():
# create   a   GraphWin
# call buildObstacles, storing   the   return   list   in   a
variable   (e.g. shapes)
# loop over the   shapes   list   and   have   each   Thing   call
its draw method
# assign   to   dt   the value   0.02
# assign   to   frame   the value   0
# create a ball, give   it   an   initial   velocity   and
acceleration, and draw   it
# start   an   infinite   loop
# if   frame. modulo   10   is   equal   to   0
# call   win.update   ()
# using checKey, if   the   user   typed   a   'q'   then   break
# if the ball   is   out   of bounds,   re-launch   it
# assign to   collided   the value   False
# for   each   item   in   the   shapes   list
代 写CS152 Project 8: Pinball WizardPython
代做程序编程语言# if the   result   of   calling   the   collision
function with the ball and   the   item   is   True
#   set collided   to   True
# if   collided   is   equal   to   False
# call the update method   of   the ball   with   dt   as
the   time   step
#   increment   frame.	
# close   the   window
if          name         ==   "      main         ":
main   ()
Doing visual updates only every   10th frame. will   make the animation   smoother. What   that   does   is   run the virtual simulation for   10 time steps and then   redraw the objects   in   their   new   positions.
You can adjust   both the time step and   how often the   visualization   is   redrawn   to   change   the   visual behavior. of the simulation.
Required   Element 2: Create a video of your pinball   machine   in action   and   upload   a   copy   along with your Google   Doc report.
T5. Create one   more shape   classCreate a   new class that   makes a   new shape with at   least two   graphics   objects.   Consider this   object to   be of type ball for the purpose of collisions.   Replace   the   ball   in   your   obstacle   scene      with the   new shape (so the new shape   should   be   bouncing   around).
Required   Element 3: Create a video which   includes your compound shape and   upload   a   copy along with your Google   Doc report.
Follow-up Questions
1.       What   is   inheritance?
2.      What does   it   mean for a child class   to   override   a   method?
3.      What   is a class variable or class   global variable?
4.      What   is a field of an   object?
Extensions
Extensions are your opportunity to customize your project,   learn something   else   of   interest   to   you, and improve your grade. The following are some   suggested   extensions,   but   you   are free   to   choose your own.   Be sure to describe any extensions you   complete   in your   report.
●          Make your pinball game interactive giving the   user   some   control   over the   visualization.      Perhaps they could launch multiple balls,   change   the   attributes   of the   balls   or   otherwise   modify the scene   in some way.
●         Create   more elaborate spaces and develop interesting additional   simulation   videos.


●         Create   more shape classes and show that they collide   and   simulate   appropriately.
●         Add the capability to   hit the   ball with a   block.
●         Create a separate scene game like   putt-putt golf and   let   the   user   shoot   the   golf   ball.
Write your project   report
Reports are   not   included   in the compressed file!   Please don’t   make the graders   hunt for your report.
You can write your report   in any word   processor you like   and   submit   a   PDF   document   in   the Google Classroom assignment folder. Or   use a   Google   Document   format.
Review the Writeup Guidelines document   in the   Labs and   Projects folder.
Your intended audience for your report   is your peers who   are   not   taking   CS   classes.
From week to week, you can assume your audience   has read   your   prior   reports.   Your   goal should   be to explain to   peers what you accomplished   in the   project and   to   give   them a sense of how you did   it. The following   is   a   list   and   description   of the   mandatory   sections you   must   include   in your report.   Do   not   include the descriptions   in your report,      but   use them as a guide   in writing   your   report.
●         Abstract
A summary of the   project,   in your own words. This should be   no   more   than   a few sentences. Give the   reader context and   identify the   key purpose   of the assignment. An abstract should define the   project's   key lecture concepts   in   your own words for a general,   non-CS audience.   It should also describe the   program's   context and output,   highlighting a couple of important   algorithmic   and/or scientific   details. Writing an effective abstract   is an important   skill.   Consider the   following questions while writing it.
○       Does   it describe the   CS   concepts   of the   project   (e.g. writing   well-organized and efficient code)?
○       Does   it describe the specific   project   application   (e.g.   generating   data)?
○       Does   it describe your solution   and   how   it was   developed   (e.g. what   code   did you write)?


○       Does   it describe the   results   or outputs   (e.g.   did   your   code   work   as   expected and what did the   results tell you)?
○         Is   it concise?
○       Are all   of the terms well-defined?
○       Does   it   read   logically   and   in   the   proper   order?
●         Methods
The   method section should describe   in clear sentences (without   pasting   any   code) at least one example of your own   computational thinking   that   helped   you   complete your project. This could   involve   illustrating   how a key   lecture   concept   was applied to creating an image,   how you   solved   a   challenging   problem,   or   explaining an algorithmic feature that   is essential to your program   as well   as why   it   is so essential. The explanation should be   suitable for   a   general   audience   who      does   not   know   Python.
●         Results
Present your results   in a clear manner   using   human-friendly   images or   graphs labeled with captions and   interpreted for a general audience such   as your   peers   not   in the course.   Explain, for a general,   non-CS audience, what your output means and whether it   makes   sense.
●       Reflection   and   Follow-up   questions
Draw connections   between   lecture concepts   utilized   in this   project and real-world   problems that   interest you.   How else could these concepts apply to our everyday lives? What are some specific things   you   had   to   learn   or   discover   in   order to complete the   project?   Look for a set of short answer questions   in   this section of the report   template.
●       Extensions   (Required   even   if you did   not   do   any)A description of any extensions you undertook,   including text output   or   images   demonstrating those extensions.   If you added any modules, functions, or   other   design components,   note their structure and the algorithms you   used.
●       References/Acknowledgements    (Required even   if there   are   none)
Identify your collaborators,   including TAs and   professors.   Include   in that   list   anyone whose code you   may have seen, such as   those   of friends who   have   taken the course   in a   previous semester. Cite any   other sources,   imported   libraries, or tutorials you used to complete   the   project.
Submitting your Project   Report and Code
Turn   in your code   by zipping the file and uploading   it to   Google   Classroom.   When submitting, double check the following.
1.       Is your name   at   the   top   of   each   Python   file?
2.       Does every function   have a docstring (‘’’ ‘’’)   specifying   what   it   does?
3.      All your code   is   in your Project   08 folder?
4.       Have you checked to   make sure you   have   included all   required   elements   and   outputs   in   your project   report?
5.       If you   have done an   Extension,   have you   included this   information   in your   report   under   the   Extension   heading?   Even   if you   have   not done any extensions,   include a section   in   your report where you   state   this.
6.       Have you acknowledged any help you   may   have   received from   classmates,   your instructor, the TAs, or outside sources (internet,   books, videos,   etc.)?   If you   received   no   help at all,   have you   indicated that under the Sources   heading   of the   report?





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
