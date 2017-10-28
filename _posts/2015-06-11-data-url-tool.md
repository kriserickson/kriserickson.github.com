---
layout: post
title: "Data Url Display"
description: "I needed a quick way to display a dataUrl as an image... "
category: Tool
tags: [DataUrl, Tools]
---


### Data Url Viewer ###

I needed a quick and dirty way to display a dataUrl as an image...   

<textarea id="dataUrlTextarea" style="width: 1020px; height: 400px; margin: 0 auto 20px;"></textarea>

<input type="button" id="dataUrlButton" value="Show Data Url">

<span id="imageResultText"></span>
<img id="imageResult" style="width: 100%"/>

<script src="//ajax.googleapis.com/ajax/libs/jquery/2.1.0/jquery.min.js"></script>

<script>
$('#dataUrlButton').click(function() {
    var dataUrl = $('#dataUrlTextarea').val();
    if (dataUrl.substr(0,10) != 'data:image') {
      $('#imageResultText').html('Does not appear to be a valid DataUrl, should be being with <code>data:image/(png|gif|jpeg)');      
    } else {
      var img = new Image();
      img.onload = function() {
        $('#imageResult').attr('src', dataUrl);
        $('#imageResultText').html('Width: ' + img.width + '<br/>Height: ' + img.height);
      } 
      img.onerror = function(e) {
        $('#imageResultText').html('Does not appear to be a valid image: ' + e);
      }
      
      img.src = dataUrl;
      
    }
});
</script>