---
layout: post
title:  "Storylines"
date:   2015-11-05
categories: devlog
---
I've made lots of progress since the last update, so I'll post a few of the things I've worked on all at once. 

I've implemented a basic Bootstrap layout in my templates so that the site isn't just plaintext debug garbage. I've also put the project up on Github: <a href="https://github.com/mkeating/pulp">https://github.com/mkeating/pulp</a>

The main functionality I've added is a storyline builder. This allows users to link to any panel in a story (not just the first one), and the chain of panels leading from the the origin will be generated and added to their interface. 

The URL structure is: /story/[some panel id]. If the ID is of the origin panel, great, it just shows that one. If it's not an origin panel, then a storyLine object is created by starting at the given ID and crawling up the parent panels until an origin panel is hit. It's accomplished with this template helper: 

<pre><code>

storyLine: function() {
	var panel = Panels.findOne({_id: this.panelID});
	var storyLine = [panel];
	if(panel.origin == false){
	    var origin = false;
	    var lastPanel;
			
		while(origin == false){
			lastPanel = Panels.findOne({_id: panel.parentPanel});
		    storyLine.unshift(lastPanel);
			
		    if (lastPanel.origin == true){
		        origin = true;
		    }
			
			panel = lastPanel;
		}
	}
	return storyLine;
}

			   </code></pre>