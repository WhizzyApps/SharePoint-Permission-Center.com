---
title: "Permission Center web part"
date: 2021-03-01T14:38:53-06:00
draft: false
layout: list
---
<!-- header -->
{{< rawhtml >}}
    <div style="display:flex;">
        <div style="text-align:center;">
            <h3>Overview</h3>
            <img class="myImg" onClick="openImage(event)" src="/images/Overview.png" style="flex-shrink:1;width:94%;"/>
        </div>
        <div style="text-align:center;">
            <h3>Demo</h3>
            <img class="myImg" onClick="openImage(event)" src="/images/Overview.gif" class="imageText"/>
        </div>
        <!-- The Modal -->
        <div id="myModal" class="modal">
            <span class="close">&times;</span>
            <img class="modal-content" id="img01">
            <div id="caption"></div>
        </div>
    </div>
    <script>
        //add eventlistener to all images
        const openImage = (event) => {
            console.log(event.target);
            modal.style.display = "block";
            modalImg.src = event.target.src;
            }
        // Get the modal
        var modal = document.getElementById("myModal");
        // Get the image and insert it inside the modal - use its "alt" text as a caption
        var img = document.getElementById("myImg");
        var modalImg = document.getElementById("img01");
        var captionText = document.getElementById("caption");
        // Get the <span> element that closes the modal
        var span = document.getElementsByClassName("close")[0];
        // When the user clicks on <span> (x), close the modal
        span.onclick = function() { 
        modal.style.display = "none";
        }
    </script>
    <hr>
    <h2 style="background-color:#F0F2F4;padding:1rem;">The web part makes it easier for site owners and users to answer the following questions:</h2>
    <div class="imageTextContainer">
        <div class="imageText">
            <h2>Who has access to a site collection and with what permission level?</h2>
            <h2>What are the members of a SharePoint group including members of nested Azure groups?</h2>
        </div>
        <div style="flex-shrink:0;">
            <img class="myImg" onClick="openImage(event)" src="/images/01.png" />
        </div>
    </div>
    <hr>
    <div class="imageTextContainer">
        <div class="imageText">
            <h2>Why is a person member of a particular group?</h2>
            <h2>What is the group nesting hierarchy of SharePoint and Azure groups?</h2>
        </div>
        <div style="flex-shrink:0;">
            <img class="myImg" onClick="openImage(event)" src="/images/02.png" />
        </div>
    </div>
    <hr>
    <div class="imageTextContainer">
        <div class="imageText">
            <h2>What (hidden) groups do exist from shared documents and folders in the site?</h2>
            <h2>What other (hidden) groups do exist without any assigned permission level?</h2>
        </div>
        <div style="flex-shrink:0;">
            <img class="myImg" onClick="openImage(event)" src="/images/03.png" />
        </div>
    </div>
    <hr>
    <div class="imageTextContainer">
        <div class="imageText">
            <h2>How can I navigate to the classic SharePoint pages to manage groups and permissions?</h2>
        </div>
        <div style="flex-shrink:0;">
            <img class="myImg" onClick="openImage(event)" src="/images/04.png" />
        </div>
    </div>
    <hr>
    <div class="imageTextContainer">
        <div class="imageText">
            <h2>How can I quickly change the group membership of users?</h2>
        </div>
        <div style="flex-shrink:0;">
            <img class="myImg" onClick="openImage(event)" src="/images/05.png" style="max-width:600px"/>
        </div>
    </div>
{{</rawhtml >}}
