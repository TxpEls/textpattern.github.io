h1. My dates look like 'Y m d'! [todo]

The format characters changed around the RC3 release. The date() formats like 'Y-m-d' no longer work; they now use "strftime() format characters":http://us3.php.net/manual/en/function.strftime.php instead.

The simplest fix is to go to textpattern > admin > preferences, select a new date format, and save the settings.
