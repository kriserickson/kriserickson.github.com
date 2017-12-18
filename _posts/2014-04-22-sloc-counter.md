---
layout: post
title: "SLOC Counter"
description: "I needed a quick way to count the lines of code in a program, skipping empty lines and ignoring commented lines so I
could get an estimate of how many lines of code a Library used (I have a current interest in SLOC and complexity).  I
searched online to find such a beast and was surprised that the only online Line of Code Counters I could find didn't
take comments or whitespace into account.  Github does a nice job of this, but not every ... "
category: Tool
tags: [SLOC, LOC, Tools]
---


### (SLOC/LOC) Line of Code Counter ###

I needed a quick way to count the lines of code in a program, skipping empty lines and ignoring commented lines so I
could get an estimate of how many lines of code a Library used (I have a current interest in SLOC and complexity).  I
searched online to find such a beast and was surprised that the only online Line of Code Counters I could find didn't
take comments or whitespace into account.  Github does a nice job of this, but not every library I was interested
in had their code in a single file.  I figured how long could a SLOC counter take to write, and the answer was 11 minutes,
so here it is, maybe you will find some use in it too:

<textarea id="slocTextarea" style="width:1020px; height: 400px; margin: 0 auto 20px"></textarea>

<span id="countResult">Number of lines: </span>

<input type="button" id="countButton" value="Count Lines of Code">

<script src="//ajax.googleapis.com/ajax/libs/jquery/2.1.0/jquery.min.js"></script>
<script>
function getCommentState(line) {
    var commentEnd = /.*\*\//;
    var match = line.match(commentEnd);
    if (match) {
        var commentStart = /.*\/\*/;
        line = line.substr(match[0].length);
        match = line.match(commentStart);
        if (match) {
            return getCommentState(line.substr(match[0].length));
        }
        return false
    }
    return true;
}

$('#countButton').click(function() {
    var allLines = $('#slocTextarea').val();
    var arrayOfLines = allLines.match(/[^\r\n]+/g);
    var inComment = false;
    var commentLine = /^\s*\/\//;
    var commentStart = /^\s*(\S*)\s*\/\*/;
    var startSearch;
    var lineCount = 0;
    for (var i = 0; i < arrayOfLines.length; i++) {
        var line = arrayOfLines[i];
        if (inComment || !commentLine.test(line)) {
            if (!inComment) {
                var match = line.match(commentStart);
                if (match) {
                    inComment = true;
                    if (match[1]) {
                        lineCount++;
                    }
                    startSearch = match[0].length;
                } else {
                    lineCount++;
                }
            }  else {
                startSearch = 0;
            }
            if (inComment) {
                inComment = getCommentState(line.substr(startSearch));
            }

        }
    }
    $('#countResult').text('Number of lines: ' + lineCount);
});
</script>