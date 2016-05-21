---
layout: post
title:  "Using the collection for global UI updates"
date:   2015-12-10
categories: devlog
---

One of the challenges of implementing the "impressionist" branching option (turning individual words in a text into paths the reader can follow, as opposed to the explicit "choice" buttons) was propagating relatively minor UI updates to all users quickly. Meteor handles client side UI updating with UI.update(params(usually a dom element inserted)), but this of course will only affect the interface for that user. 

To communicate UI changes to all users, I had to write to the collection. This at first seemed excessive to me, but Mongo apparently handles it quite well, and I saw no performance issues. I basically added a "locked" class to a word clicked by a user, preventing other users from interacting with it.


<pre><code>
	var placeholderID = Random.id();

    //console.log(placeholderID);
				
	Session.set('pendingImpressionWord', placeholderID);
	//console.log(Session.get('pendingImpressionWord'));
				
	$(event.currentTarget).addClass('locked');
	$(event.currentTarget).attr({'id': placeholderID, 'lockedBy': Meteor.userId()});
</code></pre>

The word is freed up when the user submits their story, or cancels. 

Not sure how this would scale, but that's a concern that's outside the scope of this project. 