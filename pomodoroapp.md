---
title: PomodoroApp
layout: default
---

{% capture pomodorotechnique %}{% include outbound.html href="http://pomodorotechnique.com" innerHTML="Pomodoro technique" %}{% endcapture %}
{% capture iTomato %}{% include outbound.html href="https://itunes.apple.com/hk/app/itomato/id368353070?mt=8" innerHTML="iTomato" %}{% endcapture %}
{% capture Download %}{% include outbound.html href="https://itunes.apple.com/hk/app/pomodoroapp/id705103149?mt=12" innerHTML="<img src='/images/itunes/Mac_App_Store/Download_on_the_Mac_App_Store_Badge_US-UK_165x40_0824.png' />" %}{% endcapture %}
{% capture GoogleResult %}
https://www.google.rs/search?q=tomato+icon&tbm=isch&tbs=simg:CAQSYgmi7t3Z317r7RpOCxCwjKcIGjwKOggBEhSrBtUGrQa8BtoG1AbOBsMGwQbFBhogo5ZNXvuWJxawWWykv6ztrLmVBn0W9sQ_17IWJn6hGVbkMCxCOrv4IGgAMIS9EX0xgGaBq&sa=X&ei=gU8lUqDYIY7PsgaBiICYDw&ved=0CCQQ2A4oAQ&biw=1280&bih=635#facrc=_&imgdii=_&imgrc=WFI4WXXkZixywM%3A%3BLmbf6ofZWWouPM%3Bhttp%253A%252F%252Fa4.mzstatic.com%252Fus%252Fr1000%252F082%252FPurple%252Fv4%252F0c%252Fc1%252F2c%252F0cc12c49-b6a7-0dc9-b0d4-435024a3b953%252Fmzl.iebcfoso.png%3Bhttps%253A%252F%252Fitunes.apple.com%252Ftw%252Fapp%252Fthrow-tomatoes%252Fid576215048%253Fl%253Dzh%2526mt%253D8%3B1024%3B1024{% endcapture %}
{% capture This %}{% include outbound.html href=GoogleResult innerHTML="This" %}{% endcapture %}
{% capture Contact %}{% include outbound.html href="mailto:pomodoroapp@jamztang.com" innerHTML="contact me" %}{% endcapture %}

# PomodoroApp

<script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0],p=/^http:/.test(d.location)?'http':'https';if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src=p+'://platform.twitter.com/widgets.js';fjs.parentNode.insertBefore(js,fjs);}}(document, 'script', 'twitter-wjs');</script>

<img src="/images/pomodoroapp/icon.png" />

_PomodoroApp_ is the simplest OSX app to let you to have one click toggle between count down timing sessions. The timer will enter debit mode and continues to count after a session ends.

### The Story

It started since I know about {{ pomodorotechnique }}. There's bunch of timer and pomodoro apps on iOS AppStore - {{ iTomato }} is one of my favourite. However, in practice it wasn't ideal to have my phone dedicated as a timer while I am doing iOS development. I went through the "pomodoro" list on Mac AppStore, trying from free ones to the paid ones, there just isn't a single simple enough tool that worked for me. That's how I decided to start my own implementation.

Since this is a one-day pet project for an iOS developer, I didn't manage to do a brand new icon for it. {{ This }} is where I got the widely used icon from, if you're the author of this design please {{ Contact }} for attributions. Any voluteers who might be interested to signup for this icon design would be very much appreciated, I'll be very happy to put credits here as well as in the app's about page.

{{ Download }}

If you like this app, please help spread this project!

{% capture facebooklike %}<iframe
src="//www.facebook.com/plugins/like.php?href=http%3A%2F%2Fjamztang.com%2Fpomodoroapp&amp;width=450&amp;height=46&amp;colorscheme=light&amp;layout=button_count&amp;action=like&amp;show_faces=false&amp;send=true&amp;appId=514720901947348"
scrolling="no" frameborder="0" style="border:none; overflow:hidden;
width:450px; height:46px;" allowTransparency="true"></iframe>{% endcapture %}

{% capture tweetbutton %}<a href="https://twitter.com/share" class="twitter-share-button" data-text="PomorodoApp - The simplest app for practicing pomodoro technique." data-via="PomodoroApp">Tweet</a>{% endcapture %}

{{ tweetbutton }}{{ facebooklike }}

