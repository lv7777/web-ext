# Web-ext

This is a command line tool to help build, run, and test
[web extensions](https://wiki.mozilla.org/WebExtensions).

Ultimately, it aims to support web extensions in a standard, portable,
cross-platform way. Initially, it will provide a streamlined experience for developing
[Firefox web extensions](https://developer.mozilla.org/en-US/Add-ons/WebExtensions).

## Should I Use It?

This tool may require using a
[nightly build](https://nightly.mozilla.org/) of Firefox and is initially
intended to develop web extensions, a platform which is not yet stable in Firefox.
If you are looking to develop an add-on that runs in older versions of Firefox,
consider [jpm](https://github.com/mozilla-jetpack/jpm/).

## Get Involved

Hi! This tool is under active development. To get involved you can watch the repo,
file issues, create pull requests, or ask a question on
[dev-addons](https://mail.mozilla.org/listinfo/dev-addons).

## Some Questions and Answers

### Why do we need a command line tool?

This is a great question and one that we will ask ourselves for each new web-ext
feature. Most web extension functionality is baked into the browsers
themselves but a complimentary command line tool will still be helpful.
Here is a partial list of examples:

* File watching.
  * When you edit a file, you may need to trigger certain commands (tests,
    installation, etc).
* Integrating with services.
  * Mozilla offers some useful services such as
    [linting](https://github.com/mozilla/addons-linter) and
    [signing](http://olympia.readthedocs.org/en/latest/topics/api/signing.html)
    extensions.

### Why not patch jpm for web extension support?

First, note that [jpm](https://github.com/mozilla-jetpack/jpm/) is still
actively maintained by Mozilla right now.
We decided not to patch jpm for web extension support (See
[jpm issue 445](https://github.com/mozilla-jetpack/jpm/issues/445),
[discussion](https://mail.mozilla.org/pipermail/dev-addons/2015-December/000230.html)).
Here's why.

Mozilla built [cfx](https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/cfx)
then deprecated it for jpm and now we're proposing a new tool.
I know this is frustrating for developers but web extensions mark a major
turning point. It would be an arduous task to wedge its feature set and
simplified development process into jpm.

Pros of creating a new tool:

* By creating a new tool that focuses on the [emerging] web extension standard,
  we have a better chance of interoperating with other platforms, such as
  [Google Chrome](https://developer.chrome.com/extensions) or
  [Opera](https://dev.opera.com/extensions/).
  It would be hard to do that while preserving compatibility in jpm.
* Creating SDK-based add-ons was overly complicated. With web extensions you no
  longer need to convert your source into legacy artifacts and you won't need
  boostrapping scripts.
* There are superior features in Firefox now for developing extensions such
  as [loading](https://blog.mozilla.org/addons/2015/12/23/loading-temporary-add-ons/)
  from source code instead of a packaged XPI. It will be
  easier to reimagine a new tool around these work flows rather than
  adjust jpm's existing work flows.
* jpm's functional tests are slow, brittle and hard to run. There are flaky
  time-outs and we've run out of *low hanging fruit* fixes at this point.
* Most of jpm's code was not designed to be unit testable which makes it hard to
  maintain and refactor.
* jpm's code was written in ES5 which is cumbersome after coming from the ES6
  Firefox code base or from most other languages with modern conveniences
  (Python, Ruby, etc).
* Some core functionality of jpm can be extracted and re-used in the new tool.

Cons of creating a new tool:

* Firefox extension developers will have to interrupt and re-arrange their work flows.
* Developers of existing add-ons will need to port to web extensions sooner rather than later.
* The web-ext tool will require some ramp-up time for scaffolding.
* The community of jpm contributors will need to shift focus to web-ext.
