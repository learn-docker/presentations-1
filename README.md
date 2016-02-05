# presentations
Official Docker Training

## Overview

This repository contains all of the modules and presentation definition files for the official Docker training programs.

This content is compiled and served using the **docker-present** RevealJS engine located here: https://github.com/docker-training/docker-present

## Modules and Presentations

Separating content, presentation definitions, and templating provides several advantages over creating one-file RevealJS presentations.

- All content is split into separate smaller modules. One topic or concept per module. Examples:
  - Introduction to Docker
  - Installing Docker
  - Container Concepts
  - Dockerfiles
  - etc...
- Presentation definition files are created to specify which modules will be compiled into a final presentation. These are plain text files with a list of modules (in order) to compile into the final presentation.

- Theme/Templating updates: All presentations use one common theme (Want to change or update your theme? - Edit the base html/css and all presentations are automatically updated).  See the templates section in the [docker-present README.md](https://github.com/docker-training/docker-present#templates)

Structuring projects this way makes it quick & easy to remove/include different topics/modules for talks or presentations. Much quicker than creating new presentations by copying & pasting sections of slides from existing presentations.

## Project Structure

```
kizbitz@docker:/git/docker.inc/presentations$ tree
.
├── contents.md
├── CONTRIBUTING.md
├── LICENSE
├── MAINTAINERS.md
├── modules
│   ├── example1
│   │   ├── images
│   │   │   └── small_v.png
│   │   └── slides.html
│   ├── example2
│   │   ├── images
│   │   │   └── small_v.png
│   │   └── slides.md
│   └── example3
│       └── slides.html
├── presentations
│   ├── presentation1
│   ├── presentation2
│   └── presentation3
└── README.md
```

Important files and directories:

- **contents.md**: Table of contents for Presentations and Modules
- **modules** directory: Directory containing all separate modules
- **presentations** directory: Directory containing the presentation definition files
- **CONTRIBUTING.md**: Contributing guidelines

## Creating new modules

To create a new module:

- Within the existing modules directory create a subdirecty with the name of your topic
  - `cd modules`
  - `mkdir docker-orchestration`
  - `cd docker-orchestration`
- Create either a **slides.md** or a **slides.html**  (Only one per module, but whichever you prefer)
  - `touch slides.md`
- If your module will include any images, create a subdirectory for your images. All images will be stored in this directory
  - `mkdir images`

Your final directory structure for your new module should look like:

```
kizbitz@docker:/git/docker.inc/presentations$ tree modules
modules
├── docker-orchestration
│   ├── images
│   │   └── image1.png
│   │   └── image2.png
│   └── slides.md
```

### HTML or Markdown?

There are advantages and disadvantages to both:

Markown:

None of the advanced features of RevealJS are available (Using background images, transistions, etc...) but:

- It's easier to read
- Quicker to create, edit, and modify
- Rendered correctly in Github (incuding images)

HTML:

The full range of RevealJS features available for use but:

- It's harder to read and more time consuming to create, edit, and modify
- Images are not rendered when viewing the file in Github

#### Using a slides.md (markdown) file

The following rules apply when using markdown (slides.md):

- Embedded images always use the format/path: `![name](images/filename.png)` - This will always display correctly in Github and the engine will modify the path before serving the presentation
- To separate slides use three dash characters: `---`
- To create vertical slides use four dash characters: `----`
- To add speaker notes use **Note:** - `Note: This is an example speaker note`

#### Using a slides.html file

The following rules apply when using an HTML file:

- Embedded images always use the format/path: `<img src="images/filename.png">` - The engine will modify the path before serving the presentation
- **Important**: Because of the way the **docker-present** engine has been coded the **only** html required in the slides.html file is the RevealJS `<section></section>` elements. The engine takes this file and compiles it with any other specified modules into the final index.html file that it serves. 

An example slides.html:

```
vagrant@docker:/git/docker.inc/presentations/modules/example1$ cat slides.html
<section>
    <h1>Example 1</h1>
</section>

<section>
        <h2>Example Image</h2>
        <img src="images/small_v.png">
</section>

<section>
    <h1>Reveal.js</h1>
    <h3>The HTML Presentation Framework</h3>
    <p>
        <small>Created by <a href="http://hakim.se">Hakim El Hattab</a> / <a href="http://twitter.com/hakimel">@hakimel</a></small>
    </p>
</section>
```

The base HTML template the engine uses is located here: https://github.com/docker-training/docker-present/blob/master/present/templates/index.html

For instructions on modifiying your base HTML template and theme see: [Templates](https://github.com/docker-training/docker-present#templates)

## Presentations

To specify the modules to server in your presentations create a plain text file with the name of your presentation in the presentations directory:

```
kizbitz@docker:/git/docker.inc/presentations$ tree presentations
.
├── presentations
│   ├── presentation1
│   ├── presentation2
│   └── presentation3
```

#### Required

The following rules apply when creating your presentation files:

- The first line of the file **must** be a comment (Line that starts with #) which should be a short description of the presentation
- At least one module name (a subdirectory of modules) must be listed

#### Optional

- Multiple comment lines (All lines must begin with the **#** character)
- Blank lines
- Multiple modules listed (One module per line)

Notes:

- Modules will be compiled into the final presentation in the order listed
- The engine will merge all listed modules into the final index.html (whether or not the slides were created using HTML or Markdown)

#### Example presentations files

If we have 3 modules defined:

```
kizbitz@docker:/share/git/docker.inc/presentations/modules$ tree modules
modules
├── example1
│   ├── images
│   │   └── small_v.png
│   └── slides.html
├── example2
│   ├── images
│   │   └── small_v.png
│   └── slides.md
└── example3
    └── slides.html
```

Create a presentation with modules **example1** and **example3**:

```
kizbitz@docker:/share/git/docker.inc/presentations/presentations$ cat presentation1
# All presentation files require a short description on first line

example1
example3
```

Create a presentation with modules **example3** and _then_ **example2** (reverse the order):

```
kizbitz@docker:/share/git/docker.inc/presentations/presentations$ cat presentation2
# This is my example description

# An extra comment line

example3
example2
```

or all three modules:

```
kizbitz@docker:/share/git/docker.inc/presentations/presentations$ cat presentation3
# All modules included
example1
example2
example3
```

## Running a Presentation

To run your presentations refer to the instructons for [docker-present](https://github.com/docker-training/docker-present)
