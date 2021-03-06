\\nAs long as this page is under development, we recommend visiting the
[FAQ pages on textpattern.com](http://textpattern.com/faq/).

### How to display a caption with an image {#how-to-display-a-caption-with-an-image .sectionedit1#how_to_display_a_caption_with_an_image}

(This example assumes you're using a default installation of
Textpattern.)

1.  In the admin pages, click on Presentation→Forms.
2.  In the “default” form, on the third line from the top, insert the
    following code:

<!-- -->

    <txp:if_article_image>
    <txp:images auto_detect="article" >
      <txp:image />
      <txp:image_info type="caption" wraptag="div" class="img_cap" />
    </txp:images>
    </txp:if_article_image />

Save the changes when you're done.

1.  Click Content→Images and upload an image, such as this fine
    photograph of a toy car:

[![](/home/www/zendstudio/dokuwiki/bin/lib/exe/fetch.php?media=file:captioncarupload.png)](/home/www/zendstudio/dokuwiki/bin/lib/exe/detail.php?id=&media=file:captioncarupload.png)

As part of the upload, you'll notice a caption box. Type your caption
here. On the “Images” list (pictured above), note the ID number
Textpattern has automatically assigned to this image. It happens to be
“4” in this case.

1.  Click Content→Write and write an article. In the “Article image”
    box, type in the ID of the photo you wish to use with the article.
    (“4” in this case.)

[![](/home/www/zendstudio/dokuwiki/bin/lib/exe/fetch.php?media=file:captioncararticle.png)](/home/www/zendstudio/dokuwiki/bin/lib/exe/detail.php?id=&media=file:captioncararticle.png)

1.  Here's the end result!

[![](/home/www/zendstudio/dokuwiki/bin/lib/exe/fetch.php?media=file:captionfinal.gif)](/home/www/zendstudio/dokuwiki/bin/lib/exe/detail.php?id=&media=file:captionfinal.gif)
