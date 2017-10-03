# Other ways to Contribute

**Even if you are not a developer or very familiar with P4wnP1, you can still contribute to the progress of the project**  
There are several things that need to be done:
* Proofreading of the entire Wiki for grammatical/informational errors. We are just humans like you. ;-)  
* Since this list isn't the central ToDo list, you will find up-to-date Wiki todo list [here](../ToDo.md).

## Styleguide
This repo uses the default github-webinterface characters for styling
* \`[code]\` singleline code
* \`\`\`[multiline code]\`\`\` multiline code
* `*` unordered lists
* `-` unordered list indent
* `1.` ordered list
* `---` horizontal line
* `![alt-text](url)` image
* `[text](url)` hyperlink
* `**text**` bold
* `_text_` italic
* `[display-name](page-name.md)` internal link

!!! note
    internal links use relative links instead of absolute.
    Use `../` to access the parent directory. So if you have this directory structure,
```
├── Backdoor-Subfolder
│   ├── Backdoor-Commands.md (the file you are editing)
│   └── Backdoor-Payload.md
├── Frontdoor-Payload.md
├── Payload-Home.md
├── Stealing-Browser-Credentials.md
└── Windows-10-Lockpicker.md (the file you want to link to)
```
you use `[<text to display>](../Windows-10-Lockpicker.md)` to link to Windows-10-Lockpicker.md

### Python-Markdown extensions
This Wiki uses a couple of extensions supported by [material](https://squidfunk.github.io/mkdocs-material/):
#### TOC
If you add a new page to the Wiki, it will only show up in the sidebar if you add it in `mkdocs.yml` at the correct spot.


### youtube videos
Since raw html in markdown documents is not recommended and filtered by some backends the prefered style is adding the thumbnail with the link to the video like so:
This can be done with the following syntax:  
`[![alt-text](thumbnail-link)](video-link)`  
_alt-text_ should be a descriptive name  
_thumbnail-link_ the url   `https://img.youtube.com/vi/<video_id>/0.jpg`  
_video-link_ is the link to the video   `https://www.youtube.com/watch?v=<video_id>`

**video_id** is the part after _?v=_ in every   video link.  
Example:  
`[![P4wnP1 LockPicker demo youtube](https://img.youtube.com/vi/iZXNQNIpm7s/0.jpg)](https://www.youtube.com/watch?v=iZXNQNIpm7s)`  
will be rendered to:  
[![P4wnP1 LockPicker demo youtube](https://img.youtube.com/vi/iZXNQNIpm7s/0.jpg)](https://www.youtube.com/watch?v=iZXNQNIpm7s)
