------------------------------------------------------------------------

layout: document\
category: Development\
published: true\
title: "Database schema reference"\
tags:\
- development\
- plugins\
- database\
- schema\
---

Database schema reference
=========================

Textpattern stores all data in a MySQL database. Within that database,
there are 17 tables, each containing a different collection of
information.[^1] Here we describe each table and the information it
contains, effective version 4.4.1 and later. (Since the columns can be
used to influence sorting in various list tags, non-developers may find
their descriptions useful too.)

On this page:

-   [textpattern](#sec1)
-   [txp\_category](#sec2)
-   [txp\_css](#sec3)
-   [txp\_discuss](#sec4)
-   [txp\_discuss\_ipban](#sec5)
-   [txp\_discuss\_nonce](#sec6)
-   [txp\_file](#sec7)
-   [txp\_form](#sec8)
-   [txp\_image](#sec9)
-   [txp\_lang](#sec10)
-   [txp\_link](#sec11)
-   [txp\_log](#sec12)
-   [txp\_page](#sec13)
-   [txp\_plugin](#sec14)
-   [txp\_prefs](#sec15)
-   [txp\_section](#sec16)
-   [txp\_users](#sec17)

textpattern {#sec1}
-----------

The 'textpattern' table contains the articles you create on the
****[Write](http://docs.textpattern.io/administration/content/write-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column             Type           Description
  ------------------ -------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ID                 integer        Unique, auto incremented numerical ID of the article
  Posted             datetime       Publication date and time
  Expires            datetime       Expiration date and time (defaults to 0000-00-00 00:00:00, which indicates that the article never expires)
  AuthorID           varchar(64)    Login name of the author that created the article
  LastMod            datetime       Modification date and time
  LastModID          varchar(64)    Login name of the author that modified the article
  Title              varchar(255)   Article Title
  Title\_html        varchar(255)   (reserved for future use)
  Body               mediumtext     Main article text (max 16MB), see also 'textile\_body'
  Excerpt            text           Article excerpt (max 64kB), see also 'textile\_excerpt'
  Body\_html         mediumtext     HTML version of Body
  Excerpt\_html      mediumtext     HTML version of Excerpt
  Image              varchar(255)   numerical ID of an image managed by Textpattern or URL of other image
  Category1          varchar(64)    Name of the 1th category associated with this article
  Category2          varchar(64)    Name of the 2nd category associated with this article
  Annotate           integer        Comments enabled? (0 = no, 1 = yes)
  AnnotateInvite     varchar(255)   Text used for inviting people to comment on the article
  comments\_count    integer        Number of visible comments associated with this article
  Status             integer        Status (1 = draft, 2 = hidden, 3 = pending, 4 = live, 5 = sticky)
  textile\_body      integer        Body markup (0 = raw HTML and text, 1 = textile, 2 = only convert linebreaks. Default = 1)
  textile\_excerpt   integer        Excerpt markup (0 = raw HTML and text, 1 = textile, 2 = only convert linebreaks. Default = 1)
  Section            varchar(64)    Name of the section in which this article belongs
  override\_form     varchar(64)    Textpattern 'form' containing layout used for displaying this specific article, overriding the form which is normally used to display articles. If left empty, the default layout form is used
  Keywords           varchar(255)   Comma separated list of keywords (often called 'tags') that describe this article
  url\_title         varchar(255)   Title of the article as used in the URL for the permalinked article page
  custom\_1          varchar(255)   1th Custom field (plain text)
  custom\_2          varchar(255)   2nd Custom field (plain text)
  custom\_3          varchar(255)   3rd Custom field (plain text)
  custom\_4          varchar(255)   4th Custom field (plain text)
  custom\_5          varchar(255)   5th Custom field (plain text)
  custom\_6          varchar(255)   6th Custom field (plain text)
  custom\_7          varchar(255)   7th Custom field (plain text)
  custom\_8          varchar(255)   8th Custom field (plain text)
  custom\_9          varchar(255)   9th Custom field (plain text)
  custom\_10         varchar(255)   10th Custom field (plain text)
  uid                varchar(32)    Random string used to uniquely identify this article in an RSS/Atom feed. Textpattern uses md5(uniqid(rand(),true)) to create the uid
  feed\_time         date           Creation date of the article (when you first save the article, regardless of status)

notextile.

</div>
txp\_category {#sec2}
-------------

The 'txp\_category' table contains all the categories you create on the
****[Categories](http://docs.textpattern.io/administration/content/categories-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column   Type           Description
  -------- -------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  id       integer        Unique auto-incremented ID of this category
  name     varchar(64)    Category name, used in URLs. The category 'root' is reserved (and invisible)
  title    varchar(255)   Category title
  type     varchar(64)    Type of media this category is used for: article, image, file or link)
  parent   varchar(64)    Parent category name. Determines the hierarchical place of this category compared to other categories. By default it's set to 'root' to indicate that it's a top level category.
  lft      integer        Used to maintain category hierarchy using the modified preorder tree traversal algorithm
  rgt      integer        Used to maintain category hierarchy using the modified preorder tree traversal algorithm

notextile.

</div>
txp\_css {#sec3}
--------

The 'txp\_css' table contains the style sheets created on the
****[Styles](http://docs.textpattern.io/administration/presentation/styles-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column   Type           Description
  -------- -------------- ------------------------------------------------------------------------
  name     varchar(128)   Name of the style sheet
  css      text           Style sheet contents, base64 encoded for historical reasons (max 64kB)

notextile.

</div>
txp\_discuss {#sec4}
------------

The 'txp\_discuss' table contains all the article comments output on the
****[Comments](http://docs.textpattern.io/administration/content/comments-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column      Type           Description
  ----------- -------------- -------------------------------------------------------------
  discussid   integer        Unique auto-incremented ID of this comment
  parentid    integer        ID of the article to which this comment belongs
  name        varchar(255)   Name of the person who commented
  email       varchar(50)    Email address of the person who commented
  web         varchar(255)   Website of the person who commented
  ip          varchar(100)   IP-number of the computer used to submit this comment
  posted      datetime       Date and time when this comment was submitted
  message     text           Comment message in HTML markup (max 64kB)
  visible     integer        Status (-1 = Spam, 0 = waiting for moderation, 1 = visible)

notextile.

</div>
txp\_discuss\_ipban {#sec5}
-------------------

The 'txp\_discuss\_ipban' table contains a list of all IP-numbers that
have been banned from commenting by the person who moderates
****[Comments](http://docs.textpattern.io/administration/content/comments-panel**).

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column                Type           Description
  --------------------- -------------- ----------------------------------------------------------------------------------
  ip                    varchar(255)   IP-number
  name\_used            varchar(255)   Name used by the commenter to submit the comment that cause him/her to be banned
  date\_banned          datetime       Date when the ban was imposed
  banned\_on\_message   integer        ID of the comment that caused the ban

txp\_discuss\_nonce {#sec6}
-------------------

The 'txp\_discuss\_nonce' table is an important part of the spam
protection in the commenting system. When the comment form is shown to
the user, it contains a hidden variable (nonce) with a unique code. This
code is valid for 10 minutes. If the comment form is submitted, the
nonce is looked up in this table and must exist unused with a valid
timestamp for the comment to be accepted.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column        Type          Description
  ------------- ------------- --------------------------------------------------------------------------------------------------------------------------------------------------------
  issue\_time   datetime      Date and time when the 'nonce' was created
  nonce         varchar(32)   Random alphanumeric string of text (md5)
  used          integer       Has the nonce been used for submitting a comment (0 = no, 1 = yes). A nonce cannot be used twice.
  secret        varchar(32)   Random alphanumeric string of text (md5) used to vary the name of the comment message textarea field, making it harder for spammers to submit comments

notextile.

</div>
txp\_file {#sec7}
---------

The 'txp\_file' table contains information on all the files uploaded
through textpattern. The files themselves are stored as normal files on
disk instead of in the database.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column        Type           Description
  ------------- -------------- ------------------------------------------------
  id            integer        Unique auto-incremented ID of this file
  filename      varchar(255)   Name of the file as stored on the harddisk
  title         varchar(255)   Title given to this file for display purposes
  category      varchar(64)    Name of the category associated with this file
  permissions   varchar(32)    (reserved for future use)
  description   text           File description (max 64kB)
  downloads     integer        Number of times this file has been downloaded
  status        integer        Status (2 = hidden, 3 = pending, 4 = live)
  created       datetime       Creation date and time
  modified      datetime       Modification date and time
  size          integer        File size in bytes
  author        varchar(255)   Login name of the author that added this file

notextile.

</div>
txp\_form {#sec8}
---------

The 'txp\_form' table contains all the forms, which are created on the
****[Forms](http://docs.textpattern.io/administration/presentation/forms-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column   Type          Description
  -------- ------------- --------------------------------------------------------------------
  name     varchar(64)   Form name
  type     varchar(28)   Form type: article, category, comment, file, link, misc or section
  Form     text          Contents of the form: HTML / Textpattern tags (max 64kB)

notextile.

</div>
txp\_image {#sec9}
----------

The 'txp\_image' table contains information on all the images uploaded
and managed in the
****[Images](http://docs.textpattern.io/administration/content/images-panel**)
panel. The image files are not actually stored in the database, they're
stored as normal files on the web server in the */images* folder using
the image ID as the filename (i.e. *1.png* for the main image or
*1t.png* for the corresponding thumbnail).

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column      Type           Description
  ----------- -------------- --------------------------------------------------------------------------------------
  id          integer        Unique auto-incremented ID of this image
  name        varchar(255)   Name of the image file as it was uploaded
  category    varchar(64)    Name of the category associated with this image
  ext         varchar(20)    file extension: .jpg, .gif, .png or .swf
  w           integer        Width in pixels
  h           integer        Height in pixels
  alt         varchar(255)   Alternative text for use in the ALT attribute in the HTML image tag
  caption     text           Caption for the image, used in the TITLE attribute for the HTML image tag (max 64kB)
  date        datetime       Creation date
  author      varchar(64)    Login name of the author that uploaded the image
  thumbnail   integer        Thumbnail available? (0 = no, 1 = yes)
  thumb\_w    integer        Thumbnail width in pixels
  thumb\_h    integer        Thumbnail height in pixels

notextile.

</div>
txp\_lang {#sec10}
---------

The 'txp\_lang' table contains translations for the various built-in
strings of text used on the public and administration sides of
Textpattern.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column    Type          Description
  --------- ------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  id        integer       Unique auto-incremented ID of this language string
  lang      varchar(16)   Language code (for example: en-gb for British English)
  name      varchar(64)   Unique name which identifies the language string
  event     varchar(64)   Part of Textpattern where this piece of text is typically used. This helps to keep the language strings organized for the translators. On the public side only the language strings with event 'public' and 'common' are loaded.
  data      tinytext      Translation of the language string
  lastmod   timestamp     Modification data and time of the language string

notextile.

</div>
txp\_link {#sec11}
---------

The 'txp\_link' table contains all the links and related information
created on the
****[Links](http://docs.textpattern.io/administration/content/links-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column        Type           Description
  ------------- -------------- ------------------------------------------------------------
  id            integer        Unique auto-incremented ID of this link
  date          datetime       Creation date and time
  category      varchar(64)    Name of the category associated with this link
  url           text           Link URL
  linkname      varchar(255)   Link text (plain text)
  linksort      varchar(128)   String of text which can be used to customize link sorting
  description   text           Description of the link (typically plain text)
  author        varchar(255)   Login name of the author that created this link

notextile.

</div>
txp\_log {#sec12}
--------

The 'txp\_log' table contains log entries of page requests (visits) to
your website, which are output on the ****[Visitor
logs](http://docs.textpattern.io/administration/admin/visitor-logs-panel**)
panel. Depending on your preferences, nothing is logged, just referers
or all requests. Old log entries are removed automatically.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column   Type           Description
  -------- -------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  id       integer        Unique auto-incremented ID of this log entry
  time     datetime       Date and time
  host     varchar(255)   hostname of the computer that requested the page. If DNS lookups are disabled in the preferences or if the reverse DNS lookup of the IP-number failed, the IP-number is stored instead
  page     varchar(255)   URI of the requested page
  refer    mediumtext     Whence the visitor came (Referer URL)
  status   integer        HTTP Status response code. Only status 200 (OK) is logged
  method   varchar(16)    HTTP Request method: typically POST or GET
  ip       varchar(16)    IP-number of the computer that requested the page

notextile.

</div>
txp\_page {#sec13}
---------

The 'txp\_page' table contains all the page templates you create on the
****[Pages](http://docs.textpattern.io/administration/presentation/pages-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column       Type           Description
  ------------ -------------- -------------------------------------------------------
  name         varchar(128)   Name of the template
  user\_html   text           Template contents: HTML / Textpattern tags (max 64kB)

notextile.

</div>
txp\_plugin {#sec14}
-----------

The 'txp\_plugin' table contains all the plugins you have installed,
displayed on the
****[Plugins](http://docs.textpattern.io/administration/admin/plugins-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column          Type                  Description
  --------------- --------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------
  name            varchar(64)           Plugin name
  status          integer               Status (0 = disabled, 1 = enabled)
  author          varchar(128)          Plugin author name
  author\_uri     varchar(128)          URL of the plugin author website
  version         varchar(10)           Version in dotted format
  description     text                  Short (!) description of plugin purpose (should be limited to 255 chars)
  help            text                  Documentation in XHTML format (max 64kB)
  code            mediumtext            Plugin code (PHP), sometimes modified by user on Plugin tab (max 16MB)
  code\_restore   mediumtext            Original plugin code (PHP) (max 16MB)
  code\_md5       varchar(32)           Checksum of the original plugin code
  type            integer               Where is the plugin loaded (0 = public, 1 = always, 2 = never, 3 = admin)
  load\_order     integer               Order in which this plugin will be loaded (1 = first, 9 = last). By default set to 5, which should not be changed unless you know what you're doing
  flags           smallint (unsigned)   16-bit value which signals the presence of optional capabilities to the core plugin loader. The four high-order bits 0xf000 are available for private use.[^2]

notextile.

</div>
txp\_prefs {#sec15}
----------

The 'txp\_prefs' table contains all the administration preferences
(basic, advanced, and hidden).

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column       Type           Description
  ------------ -------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  prefs\_id    integer        Unknown (always set to 1?)
  name         varchar(255)   Name that identifies this preference
  val          text           Contents/setting of this preference (max 64kB)
  type         integer        Where is it shown on the Preferences tab? (0 = basic, 1 = advanced, 2 = hidden)
  event        varchar(12)    Event to which this preference applies. Allows related preferences to be shown together on the Preferences tab
  html         varchar(64)    Type of HTML code used for display when editing this preference: yesnoradio, text\_input, gmtoffset\_select, logging, permlinkmodes, commentmode, weeks, languages, dateformats, prod\_levels or pref\_text
  position     integer        Display position of this preference among others within the same event on the Preferences tab
  user\_name   varchar(64)    login name of the user to whom this preference applies (by default set to an empty string to indicate that the preference is not bound to a specific user)

notextile.

</div>
txp\_section {#sec16}
------------

The 'txp\_section' table contains all the sections you create on the
****[Sections](http://docs.textpattern.io/administration/presentation/sections-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column          Type           Description
  --------------- -------------- ---------------------------------------------------------------------------------------------
  name            varchar(128)   Section name (used in URL)
  page            varchar(128)   Page template used for this section
  css             varchar(128)   Style sheet used for this section
  is\_default     integer        Default section for new articles? (0 = no, 1 = yes). Only one section can be set as default
  in\_rss         integer        Include articles in this section in the site's RSS or Atom XML feeds? (0 = no, 1 = yes)
  on\_frontpage   integer        Show articles in this section on the front page (0 = no, 1 = yes)
  searchable      integer        Are articles in this section searchable? (0 = no, 1 = yes)
  title           varchar(255)   Section title

notextile.

</div>
txp\_users {#sec17}
----------

The 'txp\_users' table contains information for all users, as displayed
on the
****[Users](http://docs.textpattern.io/administration/admin/users-panel**)
panel.

notextile.

<div class="tabular-data" itemscope itemtype="http://schema.org/Table">
  Column         Type           Description
  -------------- -------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  user\_id       integer        Unique auto-incremented ID of this user
  name           varchar(64)    Login name
  pass           varchar(128)   Password
  RealName       varchar(64)    Real name
  email          varchar(100)   Email address (used for sending passwords and comment notifications
  privs          integer        Privilege level (0 = none, 1 = publisher, 2 = managing editor, 3 = copy editor, 4 = staff writer, 5 = freelancer, 6 = designer). Indicates what the user is allowed to do, once logged in on the admin side
  last\_access   datetime       Date and time when the user last logged in by entering a valid username and password combination
  nonce          varchar(64)    Unique identifier used for cookie authentication (do NOT touch this in plugins!)

notextile.

</div>

[^1]: The size limits shown in the *Description* for various table
    columns (e.g. the *Body* column of the 'textpattern' table) may
    differ slightly from the actual size limits found in the tables
    created by Textpattern during installation (when a column is used in
    multiple tables, the smallest size is used). You should consider the
    limits indicated here as authoritative. When in doubt, ask a
    developer on the forum.

[^2]: See [Plugin lifecycle management and
    preferences](http://docs.textpattern.io/development/#sec9) for more
    info.