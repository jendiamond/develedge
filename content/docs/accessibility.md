---
title: "Accessibility"
date: 2019-05-19T22:37:31-07:00
draft: true
---

https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML

https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML


### Readings 
1. [WC3 Reading on Accessibility ](https://www.w3.org/WAI/fundamentals/accessibility-intro/)
2. [University of Washington Reading on Accessibility in Documents ](https://www.washington.edu/accessibility/documents/)
3. [508 Standards of Document accessibility ](https://www.cms.gov/Research-Statistics-Data-and-Systems/CMS-Information-Technology/Section508/Downloads/508-How-To-Guide-for-Microsoft-WORD.pdf)
4. [WC3 reading on Alt Text ](https://www.w3schools.com/tags/att_img_alt.asp)
5. [University of Minnesota Alt Text Reading ](https://accessibility.umn.edu/core-skills/alt-text)
6. [Penn State Alt Text Reading ](https://accessibility.psu.edu/microsoftoffice/microsoftalttags/)
7. [WC3 reading on Headers ](https://www.w3.org/WAI/tutorials/page-structure/headings/)
8. [Web Aim Semantic Structure ](https://webaim.org/techniques/semanticstructure/)
9. [Penn State Heading Reading ](https://accessibility.psu.edu/headingshtml/)
10. [Web Aim Reading on links ](https://webaim.org/techniques/hypertext/)
11. [University of Washington Guide to better links ](https://www.washington.edu/accessibility/links/)
12. [Why You Should Never Say "Click Here"  ](https://www.smashingmagazine.com/2012/06/links-should-never-say-click-here/)
13. [Why captions are important ](https://cielo24.com/2017/02/importance-of-captioning-explained/)
14. [Marketing and Captions ](https://wistia.com/learn/marketing/why-your-video-needs-captions)
15. [Info Graphic about Captions ](https://3playmedia-wpengine.netdna-ssl.com/wp-content/uploads/captioning-in-higher-education-research-study-infographic-1.pdf)

### Overview
Screen readers access the alternative text of images and allow the content and function of the image to be read to those with visual or cognitive disabilities. Alternative text is displayed in browsers in place of images if an image file is not loaded or when the user has chosen not to view images. Alternative text provides semantic meaning and description to images that can be read by search engines.

### Best Practices
* All photos and graphic images that are “essential” to understanding the content of a course page or document MUST be assigned an alternative text. Focus on consciously identifying the "content" and "function" of the image.
* The distinction between "essential" and decorative design elements varies, depending if you are a subject matter expert, a content provider, or an Instructional Designer. Subject matter experts are positioned best to describe the relevance of a photo or a graphic.
* There will always be differences in alternative text depending on the context of the image. For example, a photo of the UCLA Powell Library should be described differently when used in an architecture course versus a page offering campus directions.
* When determining appropriate alternative text for images, context is everything. The alternative text for one image may be vastly different based upon the context and surroundings of the image itself. 
* Be succinct. This means the correct content (if there is content) and function of the image (if there is a function) should be presented as concisely as possible. Typically, no more than a few words are necessary, though a short sentence or two may be appropriate.
* DO NOT use the phrases "image of..." or "graphic of..." to describe the image. It is usually apparent to screen reader users that it is an image.
* A decorative image are design elements that enhance the tone and visual consistency of a document, but do not convey meaning essential to understanding content. These include repetitions of a logo, clip art, and graphics used for design purposes only. Decorative images need alternative text but the alternative text can be “nulled” (alt="" best for webpages) or a blank space (alt=" " best for Microsoft Office).
* Use heading tags to structure all pages and documents based on main topics and subtopics, e.g. "Module 1," "Readings," "Required,” etc.
* Adhere to the correct order of headings and do not skip heading levels (e.g., go from an h2 to an h4), as screen reader users will wonder if content is missing.
* Use headings to divide blocks of text into manageable sections. By breaking up page content into smaller chunks, the material becomes more easily interpretable.  
* Do not pick a heading style based on aesthetics or because you like the font color, size, etc. Use headings to communicate structure and semantics.
* Use unique heading names for h1, and h2.
* Use descriptive hyperlinks to label the destination so it makes sense out of context.  
* Craft phrases rather than single words for link text so users with limited motor control (and mobile users) can more easily select links.
* Do not use, "Click here" to indicate a web link. This is not considered descriptive, and is ineffective for users of screen readers. Instead, describe where the link will go. For example, if you are on the UCLA website and want to inform visitors of content on the page entitled, "Latest News," don't use, "Click here" to read our Latest News," or "For the UCLA's Latest News, click here  ." Instead, consider using and hyperlinking, “UCLA's Latest News."
* When creating content on the Web, links to an external website should NOT open in a new tab or browser window.  This is recommended because screen reader users cannot utilize the "back" navigation feature immediately after opening a new browser window.  However, preserving website security is an exception to this recommendation (see next bullet).
* Learning Management Systems such as Canvas are hosted in a password protected "https" environment. The guideline for these secure sites is for all external websites to open in a new tab or window.  This practice protects the integrity of the Secure Socket Layer (SSL).
* If an image is active, i.e., if the image is inside an anchor element (<a>), then the alternative text should convey the purpose or function of the link.

WCAG 2.0 Guidelines for Audio and Video
1. If you use audio files on your Web page, a text transcript or other text-based material should be provided. WCAG 2.0 Guideline 1.2.1—"An alternative for time-based media is provided that presents equivalent information for prerecorded audio-only content."
2. If video files are used, captions or a synchronized text transcript should be provided. NOTE: Captions also benefit non-native speakers, users with audio disabled or viewers watching a video with poor quality audio. WCAG 2.0 Guideline 1.2.2—"Captions are provided for all prerecorded audio content in synchronized media, except when the media is a media alternative for text and is clearly labeled as such."
3. Video files should be embedded or displayed in a player that can be accessed by a screen reader (Links to an external site.) Links to an external site.  via keyboard commands.Accessible players include QuickTime, RealPlayer, iTunes   and YouTube  WCAG 2.0 Guideline 2.1—"Make all functionality available from a keyboard."
4. Videos that include visual information critical to comprehension should include a description of images or events   for visually impaired audiences. For example, a screencast of a software product should name the buttons and commands being used, not just say "click here". WCAG 2.0 Guideline 1.2.3—An alternative for time-based media or audio description of the prerecorded video content is provided for synchronized media, except when the media is a media alternative for text and is clearly labeled as such.
5. A lengthy piece of audio or video should not be played by default or play in an endless loop when viewing a page. Instead, the user should be able to click the play button to start the file. This provision allows users with certain cognitive, reading or motion disorders to process other content on the page as needed before viewing the content. This also prevents audio from interfering with screenreader audio. WCAG 2.0 Guideline 2.2.2—Moving, blinking, scrolling: For any moving, blinking or scrolling information that (1) starts automatically, (2) lasts more than five seconds, and (3) is presented in parallel with other content, there is a mechanism for the user to pause, stop, or hide it unless the movement, blinking, or scrolling is part of an activity where it is essential.
6. Any text displayed in a video (e.g. titles, captions) should comply with color contrast guidelines.
