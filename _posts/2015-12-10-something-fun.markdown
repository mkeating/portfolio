---
layout: post
title:  "Something Fun"
date:   2015-12-10
categories: devlog
---

Since Pulp is so heavily text-based, I wanted to include something visual, even if it was just superficial. I decided on an animated full-screen background for the landing page, with classic pulp magazine covers.

I started with a div that's within the Bootstrap container, but not within any rows or columns. Styling it like this:
	<pre><code>
				position: absolute;
				top:0;
				left:0;
				width: 100%;
				height: 100%;
				z-index: -50;
			</code></pre>


Gets us a full screen div that sits behind page content and doesn't disrupt the DOM flow. 

I created an array `covers` to hold the img urls, and run this code on startup:

<pre><code>
function animate(i){
						
	setInterval(function(){
		var counter = Math.floor((Math.random() * covers.length)+ 0);
		var direction = Math.floor((Math.random() * directions.length)+ 0);
				
		$('.animatedBackground').css(
			{
				'position': 'absolute',
				'top': '0',
				'left': '0',
				'width': '100%',
				'height': '100%',
				'z-index': '-50',
				'background-image': 'url(img/pulpcovers/'+covers[counter]+')',
				'background-repeat': 'no-repeat',
				'background-size': '20%',
				'opacity': '.9',
				
				'animation': directions[direction] + ' 7s linear infinite'
			}
		);
				
		}, 0 + i * 7000);
							
	}

</code></pre>

The `direction` is referring to some keyframe instructions that cause the zooming and opacity changes:

<pre><code>
@keyframes animatedBackgroundRightBottom {
	0%{
				
		background-position: 100% 100%; background-size: 20%; opacity: 0;
	}
	30%{
		background-position: 40% 40%; background-size: 70%; opacity: .5;
	}
	100%{
		background-position: 50% 50%; background-size: 100%; opacity: 0;
	}	
				}
</code></pre>	