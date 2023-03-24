---
redirect_from: /
published: true
---

# ELISSA Wiki

This wiki aims to document the **Elissa** project and serves as a knowledge base. It is intended to provide 
information to the testbed operators and developers and can serve as an input for documents such as technical notes or other publications.


* [testbed](testbed/testbed) links to all documents that directly adress the elissa testbed itself.
* [tutorials](tutorials/tutorials) provides tutorials for using the testbed.
* [experiments](experiments/experiments) lists setups and reports of experiments conducted onboard the testbed.

## About Elissa
Some lines about the project (TBD)
![the elissa testbed](elissa.png)

## Further reading 📕
Besides this wiki, there are some documents (slides, theses and report) describing the testbed:

* [Design and Qualification of Hardware-in-the-Loop Testbed to Experimentally Evaluate Spacecraft Proximity Operations](documents/thesislasse2020.pdf) is a student thsis that provides details regarding the Hanno Freeflyer and the GNC subsystem. [This set of Slides](documents/talklasse2020.pdf) provides a condensed version of aforementioned thesis
* [Experimentelle Charakterisierung der Dockingeigenschaften von Gecko-materialien auf einem Luftlagertisch](documents/rftp2020.pdf) describes docking tests undertaken onboard the testbed.

## Contributing to this Wiki
When adding a page to the document, think about which category is most suitable. Then create a `.md` file in the respective directory and link it to the directorys master file (the file that has the same name as the directory). It is not neccesarry to use this frontend to contribute to the wiki, you can use almost any other texteditor to write markup and `git` to add/commit your files. ** Please make sure to use standard markdown syntax, as this enables automated conversion to `.pdf`**

## Building Documentation
run one of the build scripts within the `pandoc` folder.
