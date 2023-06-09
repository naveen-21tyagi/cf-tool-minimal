# Codeforces Tool Minimal

Codeforces Tool is a command-line interface tool for [Codeforces](https://codeforces.com).

It's fast, small, cross-platform and powerful.

[Features](#features) | [Usage](#usage) | [Template Example](#template-example)

## Features

* Support Contests, Gym, Groups and acmsguru.
* Support all programming languages in Codeforces.
* Submit codes.
* Watch submissions' status dynamically.
* Fetch problems' samples.
* Generate codes from the specified template (including timestamp, author, etc.)
* Setup a network proxy. Setup a mirror host.
* Colorful CLI.

## Usage

Let's simulate a competition.

 `cf race 1136` or `cf race https://codeforces.com/contest/1136`

To start competing the contest 1136!

If the contest has not started yet, `cf` will count down. If the contest have started or the countdown ends, `cf` will use the default browser to open dashboard's page and problems' page, and fetch all samples to the local.

 `cd ./cf/contest/1136/a` (May be different from this, please notice the message on your screen)

Enter the directory of problem A, the directory should contain all samples of the problem.

 `cf gen` 

Generate a code with the default template. The filename of the code is problem id by default.

 `vim a.cpp` 

Use Vim to write the code (It depends on yourself).

 `cf submit` 

Submit the code.


```plain
You should run "cf config" to configure your handle, password and code
templates at first.

Usage:
  cf config
  cf submit [-f <file>] [<specifier>...]
  cf parse [<specifier>...]
  cf gen [<alias>]


Options:
  -h --help            Show this screen.
  --version            Show version.
  -f <file>, --file <file>, <file>
                       Path to file. E.g. "a.cpp", "./temp/a.cpp"
  <specifier>          Any useful text. E.g.
                       "https://codeforces.com/contest/100",
                       "https://codeforces.com/contest/180/problem/A",
                       "https://codeforces.com/group/Cw4JRyRGXR/contest/269760",
                       "1111A", "1111", "a", "Cw4JRyRGXR"
                       You can combine multiple specifiers to specify what you
                       want.
  <alias>              Template's alias. E.g. "cpp"
  ac                   The status of the submission is Accepted.

Examples:
  cf config            Configure the cf-tool.
  cf submit            cf will detect what you want to submit automatically.
  cf submit -f a.cpp
  cf submit https://codeforces.com/contest/100/A
  cf submit -f a.cpp 100A 
  cf submit -f a.cpp 100 a
  cf submit contest 100 a
  cf submit gym 100001 a
  cf parse 100         Fetch all problems' samples of contest 100 into
                       "{cf}/{contest}/100/".
  cf parse gym 100001a
                       Fetch samples of problem "a" of gym 100001 into
                       "{cf}/{gym}/100001/a".
  cf parse gym 100001
                       Fetch all problems' samples of gym 100001 into
                       "{cf}/{gym}/100001".
  cf parse             Fetch samples of current problem into current path.
  cf gen               Generate a code from default template.
  cf gen cpp           Generate a code from the template whose alias is "cpp"
                       into current path.

File:
  cf will save some data in some files:

  "~/.cf/config"        Configuration file, including templates, etc.
  "~/.cf/session"       Session file, including cookies, handle, password, etc.

  "~" is the home directory of current user in your system.

Template:
  You can insert some placeholders into your template code. When generate a code
  from the template, cf will replace all placeholders by following rules:

  $%U%$   Handle (e.g. naveen_21tyagi)
  $%Y%$   Year   (e.g. 2019)
  $%M%$   Month  (e.g. 04)
  $%D%$   Day    (e.g. 09)
  $%h%$   Hour   (e.g. 08)
  $%m%$   Minute (e.g. 05)
  $%s%$   Second (e.g. 00)

Script in template:
  Template will run 3 scripts in sequence when you run "cf test":
    - before_script   (execute once)
    - script          (execute the number of samples times)
    - after_script    (execute once)
  You could set "before_script" or "after_script" to empty string, meaning
  not executing.
  You have to run your program in "script" with standard input/output (no
  need to redirect).

  You can insert some placeholders in your scripts. When execute a script,
  cf will replace all placeholders by following rules:

  $%path%$   Path to source file (Excluding $%full%$, e.g. "/home/naveen_21tyagi/")
  $%full%$   Full name of source file (e.g. "a.cpp")
  $%file%$   Name of source file (Excluding suffix, e.g. "a")
  $%rand%$   Random string with 8 character (including "a-z" "0-9")
```

## Template Example

The placeholders inside the template will be replaced with the corresponding content when you run `cf gen`.

```
$%U%$   Handle (e.g. naveen_21tyagi)
$%Y%$   Year   (e.g. 2019)
$%M%$   Month  (e.g. 04)
$%D%$   Day    (e.g. 09)
$%h%$   Hour   (e.g. 08)
$%m%$   Minute (e.g. 05)
$%s%$   Second (e.g. 00)
```

```cpp
/* Generated by powerful Codeforces Tool
 * Author: $%U%$
 * Time: $%Y%$-$%M%$-$%D%$ $%h%$:$%m%$:$%s%$
**/

#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    
    return 0;
}
```
