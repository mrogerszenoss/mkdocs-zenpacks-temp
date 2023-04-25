# LogMonitor Integration Service

## ZenPacks.zenoss.PS.LogMonitor

Contents

-   About
-   Modelers
-   Installation / Usage / Removal
-   Supported Operating Systems
-   Configuration and Usage
    -   Log Search, Directory Search, and Size Check Search components
        -   Log Search Component
        -   Directory Search Component
        -   Size Check Component
-   Advanced Log Searches
    -   Configuration Properties
        -   zAdvancedLogSearches
        -   zLogSearchMaximumSizeInMB
        -   zLogSearchTimeout
    -   String Search
        -   Linux
        -   AIX
        -   Windows
    -   DataPoint within String Search
        -   Linux
        -   AIX
        -   Windows
-   Changelog

## About

ZenPack that monitors specified files (presumably log files) or
directories for size or number of matches. This integration is limited
to the specific use cases defined below regarding search, match, and
scale limitations.

<table>
<thead>
<tr markdown="1">
<th>Prerequisite</th>
<th>Restriction</th>
</tr>
</thead>
<tbody>
<tr markdown="1">
<td>Product</td>
<td>Tested with Zenoss 6.4.1 and higher</td>
</tr>
<tr markdown="1">
<td>Required ZenPacks</td>
<td><p><code>ZenPacks.zenoss.PythonCollector&gt;=1.6.1</code> </p>
<p><code>ZenPacks.zenoss.Microsoft.Windows&gt;=2.7.3</code></p>
<p><code>ZenPacks.zenoss.ZenPackLib&gt;=2.0.0</code></p>
<p><code>ZenPacks.PS.Util&gt;=1.1.0</code></p></td>
</tr>
<tr markdown="1">
<td>Other dependencies</td>
<td>None</td>
</tr>
</tbody>
</table>

## Modelers

|                                    |                                                                |
|------------------------------------|----------------------------------------------------------------|
| **LogMonitor.AdvancedLogSearches** | Advanced Log Search components                                 |
| **LogMonitor.zProperties**         | Log Search, Directory Search, and Size Check Search components |

## Installation / Usage / Removal

Install this ZenPack following the instructions in the Zenoss Admin
Guide matching your Zenoss version.

## Supported Operating Systems

-   Windows
-   AIX (SSH Only)
-   Linux (SSH Only)
-   Solaris (SSH Only) (Only Log Search, Directory Search, and Size
    Check supported on Solaris)

**Note:** Due to a limitation of the Windows FINDSTR utility, regular
expression alternation is not supported when specifying a Search
Pattern. This means you can not specify a list of patterns for which to
search. You'd have to create multiple components to work around this. On
UNIX devices you can specify multiple patterns on new lines.

## Configuration and Usage

### Log Search, Directory Search, and Size Check Search components

There are two methods one can add these component types

1.  Manually adding via the RM web user interface, selecting the
    corresponding option in the "+" button from the lower left.

2.  Component configuration defined in a zProperty and the component is
    added as part of the model cycle.

    | Component type   | zProperty name to define configuration |
    |------------------|----------------------------------------|
    | Log Search       | zLogSearchInstances                    |
    | Directory Search | zDirectorySearchInstances              |
    | Size Check       | zSizeCheckInstances                    |

**\*NOTE**: The three component types have a "*zPropertyDefined*"
property that can be seen under details, labeled as "*Component
configured in zProperty*". This is an indicator of how the component was
added to zenoss, manually or via modeling/zProperty.

**\*\*NOTE**: If a configuration change is made
to *zLogSearchInstances*, *zDirectorySearchInstances*,
or *zSizeCheckInstances* those changes will not be applied to monitoring
until the next modeler run.

#### Log Search Component

**Description**: Simple Log Search monitoring

**Configuration parameters**:

| Parameter                                                         | Description                                                                                    |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| "ID" / "Log Search ID"                                            | Component ID value                                                                             |
| Base Path                                                         | Base directory path to apply "Filename Pattern" against                                        |
| Filename Pattern                                                  | Pattern to apply to match log file name                                                        |
| "Search Patterns" / "Array of search patterns to apply"           | Regular expressions to apply against any matching file. Each regexp separated by a line-break. |
| "No log found event" / "Generate event if log file is not found?" | Generate an event if no file matches filename pattern                                          |

#### Directory Search Component

**Description**: Search for filenames found in a Directory monitoring

**Configuration parameters**:

| Parameter                    | Description                                                                         |
|------------------------------|-------------------------------------------------------------------------------------|
| "ID" / "Directory Search ID" | Component ID value                                                                  |
| Base Path                    | Base directory path to apply "Filename Pattern" against                             |
| Filename Pattern             | Pattern to apply to match log file name                                             |
| Search Recursively           | Search for files only in the base directory or include subdirectories in the search |

#### Size Check Component

**Description**: Total size of all files in a Directory monitor

**Configuration parameters**:

| Parameter              | Description                               |
|------------------------|-------------------------------------------|
| "ID" / "Size Check ID" | Component ID value                        |
| Base Path              | Base directory path to perform size check |

## Advanced Log Searches

Advanced Log Searches allow for more flexibility in log monitoring,
including

-   two types of searches - "String" search, to track number of
    occurrences of a pattern, and "DataPoint within String" search,
    which can use a regular expression to extract a number from a
    specific string
-   Search only from the last position read
-   Graph and threshold based on the number of matches

### Configuration Properties

#### zAdvancedLogSearches

This is the main zProperty for Advanced Log Searches. When you edit this
property, a special edit dialog will pop up that allows you to add and
edit advanced log searches.

The following steps must be followed to enter and save the log searches:
1) Enter information in the fields 2) Click "Add", or "Update" (if
editing an existing search) 3) **IMPORTANT** Your new or updated search
has not been saved until you click "Submit" to update the
zAdvancedLogSearchesProperty 4) After you have clicked "Submit", you
need to either remodel the device or wait until the next modeling cycle
for the Advanced Log Search components to appear

#### zLogSearchMaximumSizeInMB

If a log file in a search is larger than the specified size (in
megabytes), the search will not be performed and a warning event will be
generated

#### zLogSearchTimeout

In Seconds. If a log search takes longer than the specified number of
seconds to return with data, the data is still stored, but a warning
event will be generated informing of how long the search took. Default
is set to a low number, as most searches should come back quickly, but a
good rule of thumb is to set it to slightly shorter than the cycle time
to guarantee that searches aren't stepping on each other.

\*\* THE FOLLOWING ZPROPERTIES ARE CURRENTLY ONLY IN USE FOR WINDOWS
SEARCHES \*\* zLogSearchSleepAfterLines, zLogSearchSleepMilliseconds
\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#
These two properties work together to help mitigate a performance hit on
the Windows server. As the search goes line by line through the log
file, the script can be set to pause every "*zLogSearchSleepAfterLines*"
lines, for "*zLogSearchSleepMilliseconds*" milliseconds. Default is set
to 1ms/2500 lines.

### String Search

#### Linux

Linux string searches are performed using grep with the switches -P (use
Perl regular expression syntax) and -c (suppress normal output; instead
print a count of matching lines).

The command used by Linux to do the search is this:

> `grep -cP SEARCH_PATTERN LOGFILE_NAME`

Anything that you enter into the "search pattern" field in the Advanced
Log Searches dialog must be able to be substituted for SEARCH_PATTERN in
the command above. So, for example, if you are only searching for one
word, the following would work:

> Search pattern: `Error`
>
> Test command: `grep -cP Error some_logfile.log`

Or a regular expression without spaces:

> Search pattern: `[0-9]+$` (a pattern that will search for a line that
> has a number at the end of the line)
>
> Test command: `grep -cP [0-9]+$ some_logfile.log`

But if you are searching for a string with spaces, you would need to
enclose it in quotes:

> Search pattern: `"Error detected"`
>
> Test command: `grep -cP "Error detected" some_logfile.log`

Or if you are searching for a string with double-quotes, you could
enclose it in single quotes:

> Search pattern: `'Error code "12345" has been found'`
>
> Test
> command: `grep -cP 'Error code "12345" has been found' some_logfile.log`

Keep in mind that everything in the search pattern will be evaluated as
a regular expression, so if you are searching for any characters that
are used in regular expressions, they will need to be escaped using a
backslash.

Here are some examples:

>
>
> | Search for:                       | Search Pattern:                       |
> |-----------------------------------|---------------------------------------|
> | Error                             | `Error`                               |
> | Error detected                    | `Error detected`                      |
> | I've got a single quote           | `"I've got a single quote"`           |
> | Here are some "double" quotes     | `'Here are some "double" quotes'`     |
> | \[ERROR\] There has been an error | `"\[ERROR\] There has been an error"` |
> | (Any line ending with a digit)    | `\d+$`                                |
>
>

#### AIX

AIX string searches are performed using egrep with the switch -c
(suppress normal output; instead print a count of matching lines).

The command used by AIX to do the search is this:

> `egrep -c SEARCH_PATTERN LOGFILE_NAME`

Anything that you enter into the "search pattern" field in the Advanced
Log Searches dialog must be able to be substituted for SEARCH_PATTERN in
the command above. So, for example, if you are only searching for one
word, the following would work:

> Search pattern: `Error`
>
> Test command: `egrep -c Error some_logfile.log`

Or a regular expression without spaces:

> Search pattern: `[0-9]+$` (a pattern that will search for a line that
> has a number at the end of the line)
>
> Test command: `egrep -c [0-9]+$ some_logfile.log`

But if you are searching for a string with spaces, you would need to
enclose it in quotes:

> Search pattern: `"Error detected"`
>
> Test command: `egrep -c "Error detected" some_logfile.log`

Or if you are searching for a string with double-quotes, you could
enclose it in single quotes:

> Search pattern: `'Error code "12345" has been found'`
>
> Test
> command: `egrep -c 'Error code "12345" has been found' some_logfile.log`

Keep in mind that everything in the search pattern will be evaluated as
a regular expression, so if you are searching for any characters that
are used in regular expressions, they will need to be escaped using a
backslash.

Here are some examples:

>
>
> | Search for:                       | Search Pattern:                       |
> |-----------------------------------|---------------------------------------|
> | Error                             | `Error`                               |
> | Error detected                    | `"Error detected"`                    |
> | I've got a single quote           | `"I've got a single quote"`           |
> | Here are some "double" quotes     | `'Here are some "double" quotes'`     |
> | \[ERROR\] There has been an error | `"\[ERROR\] There has been an error"` |
> | (Any line ending with a digit)    | `[0-9]+$`                             |
>
>

#### Windows

Windows string searches are performed by using
System.Text.RegularExpressions.Regex(SEARCH_PATTERN), comparing it to
the log file, line by line from the last position read, and generating a
count of matching lines.

The following is a stripped down version of the PowerShell commands used
to generate a string count, and can be used to test your search
patterns, replacing LOG_FILE with the log file to search and
SEARCH_PATTERN with the pattern you are testing:

    $logfile = 'LOG_FILE';
    $pattern = 'SEARCH_PATTERN';
    $stream = New-Object System.IO.FileStream -ArgumentList $logfile, 'Open', 'Read', 'ReadWrite' -ErrorAction Stop;
    $reader = New-Object System.IO.StreamReader -ArgumentList $stream, $true;
    $reader.BaseStream.Seek(0, 'Begin') | Out-Null;
    $reader.ReadLine() | Out-Null;
    $reader.DiscardBufferedData();
    $regex = New-Object System.Text.RegularExpressions.Regex($pattern);
    $search_count = 0;
    while($null -ne ($buffer = $reader.ReadLine())) { if($regex.IsMatch($buffer)) { $search_count++; } }
    $reader.Close();
    $stream.Close();
    $search_count

Anything that you enter into the "search pattern" field in the Advanced
Log Searches dialog must be able to be substituted for SEARCH_PATTERN in
the command above. So, unlike in Linux, quotes are NOT required in your
search pattern, even if there are spaces or special characters in the
pattern. To escape a single quote, double it (''). No escaping is
required for double quotes.

Keep in mind that everything in the search pattern will be evaluated as
a regular expression, so if you are searching for any characters that
are used in regular expressions, they will need to be escaped using a
backslash.

Here are some examples:

>
>
> | Search for:                       | Search Pattern:                     |
> |-----------------------------------|-------------------------------------|
> | Error                             | `Error`                             |
> | Error detected                    | `Error detected`                    |
> | I've got a single quote           | `I''ve got a single quote`          |
> | Here are some "double" quotes     | `Here are some "double" quotes`     |
> | \[ERROR\] There has been an error | `\[ERROR\] There has been an error` |
> | (Any line ending with a digit)    | `\d+$`                              |
>
>

### DataPoint within String Search

"Datapoint within string" search requires a regular expression to
extract a number from the matching string. Due to differences in
operating system implementation, different patterns must be used.

#### Linux

Linux datapoint searches are performed using grep with the switches -P
(use Perl regular expression syntax) and -o (print only the matched part
of a matching line).

The command used by Linux to do the search is this:

`grep -oP SEARCH_PATTERN LOGFILE_NAME`

This command will give you ALL matching results, while the LogMonitor
ZenPack will only return the last one found, but it will let you know if
your search pattern returns what you are expecting.

Anything that you enter into the "search pattern" field in the Advanced
Log Searches dialog must be able to be substituted for SEARCH_PATTERN in
the command above.

The recommended way to do a datapoint search in Linux is to
use **lookarounds** and the **digit character**.

`(?=sometext)` - Lookahead: "sometext" comes immediately after the
current position

`(?<=sometext)` - Lookbehind: "sometext" comes immediately before the
current position

`(?!sometext)` - Negative lookahead: "sometext" definitely does NOT come
immediately after the current position

`(?<!sometext)` - Negative lookbehind: "sometext" definitely does NOT
come immediately before the current position

For example, assuming a logfile `some_logfile.log` with the following
entry:

> `WSVR0605W: Thread &ldquo;WebContainer: 1&rdquo; has been active for 612,000 milliseconds and may be hung. There are 3 threads in total in the server that may be hung.`

A good search pattern to pull out the number of possible hung threads
might be:

`'(?<=There are)\d+(?= threads in total in the server that may be hung.)'`

And you could test that on the command line as follows:

`grep -oP '(?<=There are)\d+(?= threads in total in the server that may be hung.)' some_logfile.log`

Which should return:

`3`

Some things to notice about this pattern:

-   The significant piece here is the `\d+`. With grep -o, the lookahead
    and lookbehind will NOT be included, and only the digits in between
    will be returned
-   If we are using lookaround syntax, we need to enclose the expression
    in single or double quotes. Otherwise, we will get a syntax error
    for the unexpected `(`.

#### AIX

AIX datapoint searches use a combination of egrep and sed.

The AIX method for datapoint searches has several idiosyncracies:

-   For digits, since we cannot use Perl regular expressions, character
    class must be used, followed by an asterisk: \[0-9\]\*
-   Lookaround logic does not work; you must use a "capturing group" to
    extract the number
-   In regular expressions, a capturing group is indicated using ().
    HOWEVER, because egrep and sed have different ways that parentheses
    need to be escaped, search patterns entered into the Log Monitoring
    ZenPack use DOUBLE parentheses (())to indicate a capturing group. If
    a parenthesis is part of the text you're searching, it just needs to
    be escaped normally. \\(-   The search pattern must compensate for the entire line; anything not
    explicitly covered by the regular expression will be returned with
    the datapoint. So make sure to precede your search pattern with ^.\*
    (any number of occurrences of any characters at the beginning of the
    line) and succeed your search pattern with .\*$ (any number of
    occurrences of any characters at the end of the line)

The commands you can use to test your search pattern in AIX are:

1.  egrep 'EGREP_SEARCH_PATTERN' LOG_FILE \| sed -n -e
    's/SED_SEARCH_PATTERN/\\1/p' \| tail -1

OR

1.  egrep "EGREP_SEARCH_PATTERN" LOG_FILE \| sed -n -e
    "s/SED_SEARCH_PATTERN/\\1/p" \| tail -1

Use \#2 only if your search pattern includes double quotes. \#1 should
be used in all other circumstances.

Also notice that we have EGREP_SEARCH_PATTERN and SED_SEARCH_PATTERN.
This is due to the different ways egrep and sed use capturing groups, as
mentioned above. Because of these idiosyncracies, we have to take the
search pattern that we are entering into the LogMonitor ZenPack and
format it differently for each command.

For example, assuming a logfile `some_logfile.log` with the following
entry:

> `WSVR0605W: Thread "WebContainer: 1" has been active for 612,000 milliseconds and may be hung. There are 3 threads (total) in the server that may be hung.`

a good search pattern to pull out the number of possible hung threads
might be:

> `^.*There are (([0-9]*)) threads \(total\) in the server that may be hung.*$`

Take note that we have used (()) for our capturing group and backslashes
to escape the parentheses in the actual text. So, to test the command,
we'll need to format the egrep and sed search patterns as follows

>
>
> | Pattern:             | New format:                                                                  | What we changed:                                                                                   |
> |----------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
> | EGREP_SEARCH_PATTERN | `^.*There are ([0-9]*) threads \(total\) in the server that may be hung.*$`  | Double parentheses replaced with single                                                            |
> | SED_SEARCH_PATTERN   | `^.*There are \([0-9]*]\) threads (total) in the server that may be hung.*$` | Double parentheses replaced with escaped parentheses, backslashes removed from escaped parentheses |
>
>

Now we can test our search on the command line as follows:

`egrep '^.*There are ([0-9]*) threads \(total\) in the server that may be hung.*$' some_logfile.log | sed -n -e 's/^.*There are \([0-9]*\) threads (total) in the server that may be hung.*$/\1/p' | tail -1`

Which should return:

`3`

Here are some example patterns:

>
>
> | Search for:                                  | Expected | Search Pattern:                                                |
> |----------------------------------------------|----------|----------------------------------------------------------------|
> | There are 3 hung threads                     | 3        | `^.*There are (([0-9]*)) hung threads.*$`                      |
> | A "double" quote datapoint: 31               | 31       | `^.*A "double" quote datapoint: (([0-9]*)).*$`                 |
> | \[ERROR\] 13 errors found                    | 13       | `^.*\[ERROR\] (([0-9]*)) errors found.*$`                      |
> | A parenthesis (is) here: 47 is the datapoint | 47       | `^.*A parenthesis \(is\) here: (([0-9]*)) is the datapoint.*$` |
>
>

#### Windows

Datapoint searches in Windows also use the
System.Text.RegularExpressions object, as in the "string" search above.
However, to just test your search pattern, you can use this simpler
command, replacing TEST_STRING with a line to test against, and
SEARCH_PATTERN with your pattern:

    $matches = ''; $found = 'TEST_STRING' -match 'SEARCH_PATTERN'; $matches[0]

Anything that you enter into the "search pattern" field in the Advanced
Log Searches dialog must be able to be substituted for SEARCH_PATTERN in
the command above.

The recommended way to do a datapoint search in Windows is to
use **lookarounds** and the **digit character**.

`(?=sometext)` - Lookahead: "sometext" comes immediately after the
current position

`(?<=sometext)` - Lookbehind: "sometext" comes immediately before the
current position

`(?!sometext)` - Negative lookahead: "sometext" definitely does NOT come
immediately after the current position

`(?<!sometext)` - Negative lookbehind: "sometext" definitely does NOT
come immediately before the current position

For example, for a log entry that looks like this:

> `WSVR0605W: Thread &ldquo;WebContainer: 1&rdquo; has been active for 612,000 milliseconds and may be hung. There are 3 threads in total in the server that may be hung.`

A good search pattern to pull out the number of possible hung threads
might be:

> `(?<=There are)\d+(?= threads in total in the server that may be hung.)`

And you could test that on the command line as follows:

> `$matches = ''; $found = 'WSVR0605W: Thread &ldquo;WebContainer: 1&rdquo; has been active for 612,000 milliseconds and may be hung. There are 3 threads in total in the server that may be hung.' -match '(?<=There are)\d+(?= threads in total in the server that may be hung.)'; $matches[0]`

Which should return:3

The significant piece here is the `\d+`. With
System.Text.RegularExpressions, lookahead and lookbehind will NOT be
included, and only the digits in between will be returned

For datapoint regular expressions, double-quotes do NOT need to be
escaped. Single quotes DO need to be escaped by doubling, and other
special characters that are used in regular expressions must be escaped
by a backslash.

Here are some example patterns:

>
>
> | Search for:                      | Expected Datapoint | Search Pattern:                           |
> |----------------------------------|--------------------|-------------------------------------------|
> | There are 3 hung threads         | 3                  | `(?<=There are)\d+(?= hung threads)`     |
> | I'm a single quote datapoint: 25 | 25                 | `(?<=I''m a single quote datapoint:)\d+` |
> | A "double" quote datapoint: 31   | 31                 | `(?<=A "double" quote datapoint:)\d+`    |
> | \[ERROR\] 13 errors found        | 13                 | `(?<=\[ERROR\])\d+(?= errors found)`     |
>
>

## Changelog

1.5.0

-   Fixes:
    -   SVC-2926: Separating out the Windows SingleInteger and LogSearch
        parsersSVC-3145: add migration for wrong targetPythonClass

1.4.4

-   Fixes:
    -   SVC-2648 Fix AdvanceLogSearch, moved file pointer store to redis

1.4.3

-   Fixes:
    -   SVC-2648 Fix AdvanceLogSearch zenhub ADM causing file position
        pointer not updating

1.4.2

-   Fixes:
    -   SVC-2531: Unix's log_search datasource command update.
        Differenctial between no file match found & no pattern matches
        found in file

1.4.1

-   Fixes:
    -   SVC-2531: log_search datasource no match result fixUNIX servers
        returned a null value, thus no graph updatesWindows servers
        would "File not found" event when no matches were found

1.4.0

-   Fixes:
    -   SVC-1993: fix details display for LogSearch componentsSVC-2315:
        fix impact uncorroborated edgesSVC-1973: fix collection failure
        when target log file is missingSVC-1683: correct units for
        match_total datapoint (rate: matches per second)SVC-2485: New
        method to define Directory & File monitoring via
        zPropertiesFeatures:SVC-1974: allow for event to be generated if
        target log file is missingSVC-1683: add matchCount datapoint for
        abloute number of matches (non-rate)

 1.3.1

-   Fixes:
    -   targetPythonClass on several templates (caused errors in Zope
        when loading templates)

1.3.0

-   -   Add component to max size event.
    -   Fix usage of search_patterns property on RM 6.2


