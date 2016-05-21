---
layout: post
title:  "Interface Animations"
date:   2015-11-06
categories: devlog
---
<pre><code>
scrollToActive = function(){
	//console.log('testing global function');
	$('html, body').animate({
		scrollTop: $("#"+Session.get('activePanel')).offset().top
	}, 1000);
}

scrollToActive = function(){
	//console.log('testing global function');
	$('html, body').animate({
		scrollTop: $("#"+Session.get('activePanel')).offset().top
	}, 1000);
}

</code></pre>

Here is a quick little bit of Jquery that scrolls to the current active panel. This means that when you go to the url for a panel that's 20 panels deep in a story, the whole storyline will render, and then we'll slide down to the active panel. I'm not sure if I'll keep this interface interaction; for example, if I want to share a storyline with my friend, he would probably rather start at the beginning than have to scroll up. The auto scroll is useful, however, when picking up a story where you left off. We'll see which is better, or maybe I can do both with a parameter in the url. 