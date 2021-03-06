---
layout: document
category: Tags
published: true
title: If plugin
description: The if_plugin tag will execute the contained statements if the name attribute matches a currently installed plugin.
tags:
  - Conditional tags
---

# If plugin

On this page:

* [Syntax](#syntax)
* [Attributes](#attributes)
* [Examples](#examples)
* [Genealogy](#genealogy)

## Syntax

~~~ html
<txp:if_plugin>
~~~

The **if_plugin** tag is a *conditional* tag and always used as an opening and closing pair, like this...

~~~ html
<txp:if_plugin>
    ...conditional statement...
</txp:if_plugin>
~~~

The tag will execute the contained statements if the name attribute matches a currently installed and enabled plugin, and the current version number is equal to or greater than the `version` attribute assigned (if used).

## Attributes

Tag will accept the following attributes (**case-sensitive**):

`name="text"`
: Plugin name as defined on the [Plugins administration panel](http://docs.textpattern.io/administration/plugins-panel).

`version="number"`
: Minimum plugin version number.
: **Default:** unset.

## Examples

### Example 1: Check plugin exists before using a tag

~~~ html
<txp:if_plugin name="zem_plugin_lang" version="4">
    <txp:zem_contact to="dest@example.com" />
</txp:if_plugin>
~~~

Applies the tag `<txp:zem_contact />` if the 'zem_contact_lang' plugin is installed, activated, and the version number is equal to or greater than 4.

## Genealogy

### Version 4.3.0

`ver` attribute deprecated and renamed `version`.
