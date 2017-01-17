# Howto Section

Repository for the microbit playground [components section](https://microbit-playground.co.uk/howto/).

This repository is checked out at build time. There is a `draft` branch and a `publish` branch. All changes should be made to the `draft` branch and pulled in with a squash. `publish` then merges `draft`.

### Contributing
See [the page on the website](https://microbit-playground.co.uk/about/how-to-contribute). Submissions are welcome.

Submit an issue if you have an idea for an article.

##### A Contribution Should...
* Not contain fixes or additions to existing articles; please use 'Issues'.
* Be a pull request to the `draft` branch.
* Have a `720x420px` `.png` teaser image in `/teaser/`.
* all filename prefixed by the name of the name of the main of the `.md` file.
* Update the _Image Licensing_ section of this README.
* Licensed images used are mentioned in the `YAML` frontmatter of the `.md` file in the `acknowledgements` field if required.
* Nothing too spammy or marketty or Google juicy.

###### Optional
* For public attribution on the website, add your name and details to the author repository.

###### A Brief Note
Github is very rude! I do not mean the people but github.com.  Picture the scene: you spend an age writing an article and are filled with pride and goodness about helping kids & adults learn. When I review and start to edit it, __rejected__ or __changes requested__ appears!

Perhaps this works fine in some areas but I know there is an emotional attachment when writing learning resources.

So please, do please translate these messages from robot into Human.

### Files in Repository
The website's pages are generated from `.md` files in the main directory. The name of each `.md` file has a corresponding image in `/teaser/` of the same name.

* `/images/` -- Images used in the article.
* `/teaser/` -- Directory for teaser images & video.
* `/teaser/tiny` & `/teaser/card` -- Generated images sizes.
* `/KITCHENSINK.md` -- Examples for fomatting.

### Licensing
#### Contributions
Each submission is covered by the CC-BY-NC 3.0 licence. You retain copyright but allows the website to use it (but not make money).

#### Images


| Image Name          |  Author          |   Licence         |
|---------------------|------------------|-------------------|
| LED blink vid       | Jez              | CC0               |
| pot on breadboard   | Jez              | CC0               |
| GUIZero video       | Jez              | CC0               |
| Microbit Breakout b | Jez              | CC0               |
| 7seg-spi            | Jez              | CC0               |
| [microbit pinout]   | [Python Docs]    | MIT               |

* All Fritzing diagrams CC0 by Jez.
* All PXT screenshots CC0 by Jez.

* ??? / fair use
Excel screenshot / Bluetooth Logo / Blurred Waving Graph Image /

[microbit pinout]: https://github.com/bbcmicrobit/micropython/blob/master/docs/pin.rst
