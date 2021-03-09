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
        <img class="myImg" onClick="openImage(event)" src="/images/Overview.gif" style="flex-shrink:1;"/>
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
{{</rawhtml >}}


### The web part makes it easier for site owners and users to answer the following questions:

![](/images/01.png)

# Who has access to a site collection and with what permission level?

# What are the members of a SharePoint group including members of nested Azure groups?

![](RackMultipart20210308-4-1g1t57u_html_692e1f946e6255d4.png)

# Why is a person member of a particular group?

# What is the group nesting hierarchy of SharePoint and Azure groups?

![](RackMultipart20210308-4-1g1t57u_html_8f6fb8e4f7954901.png)

# What (hidden) groups do exist from shared documents and folders in the site?

# What other (hidden) groups do exist without any assigned permission level?

![](RackMultipart20210308-4-1g1t57u_html_318951f014f93cd.png)

# How can I navigate to the classic SharePoint pages to manage groups and permissions?

![](RackMultipart20210308-4-1g1t57u_html_65b25f705e268312.png)

# How can I quickly change the group membership of users?
