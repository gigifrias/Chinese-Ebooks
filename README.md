# Chinese-Ebooks for VOA China

DOCUMENT SET-UP
File Sizes
XHTML files larger than 300KB can crash or run very slowly some reading systems, especially older ones. The same is true of images that are larger than 10MB.

Namespaces 
Declare ePub3 specifications:
XHTML
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:epub="http://www.idpf.org/2007/ops" … >
CSS
@namespace "http://www.w3.org/1999/xhtml"; 
@namespace epub "http://www.idpf.org/2007/ops"; 

Character Encoding
Declare language encoding to match language.
Simplified Chinese: 	GB2312
Traditional Chinese: 	BIG5
Chinese (unknown): 	UTF-8
XHTML
<?xml version="1.0" encoding="BIG5"?>
<meta charset="big5" … />

CSS
@charset "big5";

Document Language
XHTML: Use language attributes rather than HTTP or meta elements to declare the default language for text processing 
For XHTML 1.0 served as text/html use the lang and xml:lang attributes
<html lang="zh-Hant" xml:lang="zh-Hant" xmlns="http://www.idpf.org/2007/ops">
For XHTML served as XML use the xml:lang attribute only
<html xml:lang="zh-Hant" xmlns ="http://www.idpf.org/2007/ops">
Add a Content-Language declaration in a meta element to the head of your document.
<meta http-equiv="Content-Language" content="zh-Hant"/>
The language of any text content contained within an SVG image should always be set to ensure that assistive technologies render the content properly.

Page Margins
CSS: Use pixel measurements @page and body for consistency. 
Note that these values will produce extra-wide margins on the Kindle Fire, because the view for that e-reader is narrow already.
@page {
     margin: 30px;
}
 
body, div, dl, dt, dd, ul, ol, li, h1, h2, h3, h4, h5, h6, p, pre, code, blockquote {
	margin: 0;
	padding: 0;
	border-width: 0;
}

OPF File
XML: Declare ePUB3 namespace in metadata 
<metadata xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:opf="http://www.idpf.org/2007/opf">
Add additional authors or editors as needed:
Include all additional assets in manifest
XML: Always include guide in OPF file after spine section.
<!– for ePub –>
<guide>
<reference href=”Cover.html” type=”cover” title=”"/> <!– Specified book Cover –>
<reference href=”book002.html” type=”toc” title=”Table of Contents”/> <!– Link to TOC  page –>
<reference type=”other.ms-firstpage” title=”" href=”title.html”/> <!– Specifies on which page book should get open when book is opened first time –>
</guide>


Semantic Structure
Make the ePUB more accessible by creating non-visual structure in HTML with semantic inflection to define the nature of structural markup.
Cover
The publications cover(s), jacket information, etc.
<body epub:type="cover">

Front Matter
Preliminary material to the main content of a publication, such as tables of contents, dedications, etc.
<body epub:type="frontmatter">

Title Page
<section epub:type="titlepage">
  …
</section>

Copyright information
<section epub:type="copyright-page">
  …
</section>

Foreword
<section epub:type="foreword">
  …
</section>

Introduction
<section epub:type="introduction">
  …
</section>

Table of Contents
<section epub:type="toc">
  …
</section>



Body Matter
The main content of a publication.
<body epub:type="bodymatter">

Part
A major structural division of a piece of writing, typically encapsulating a set of related chapters.
<section epub:type="part">
  …
</section>

Chapter/Subchapter
<section epub:type="chapter">
  …
</section>

Endnote reference
<p>lorum ipsum.<a epub:type="noteref" href="#en01">1</a></p>

Back Matter
Ancillary material occurring after the main content of a publication including endnotes. epub:type=“noteref” and epub:type=“footnote” are pop-up notes which may crash the application if not supported by a device, use epub:type=“rearnote” to avoid.
<body epub:type="backmatter">

Endnotes section
<section epub:type="rearnotes">
  <h1>Endnotes</h1>
  <section id="en01" epub:type="rearnote">
        …
  </section>
  …
</section>


CONTENT
Cover
Cover images should be JPEGs at 120 DPI. Dimensions vary per device but the image should always be taller than it is wide (portrait orientation) with a ratio around 1:1.3 to 1:1.65.
CSS: Cover image should resize to fill as much of the display of the eBook reader as possible and avoid distortion or clipping.
img.cover-image {
	max-width: 100%;
	max-height: 100%;
	display: block;
}

Navigation + TOC
Create navigation within a regular HTML document by using nav tag. 
EPUB 3 Publications may include an NCX document for EPUB 2 Reading System forwards compatibility purposes. 

HTML: Use the landmarks epub:type attribute throughout the publication to denote the document structure for navigation.
<nav epub:type="landmarks">
	<ol>
		<li><a epub:type="cover" href="cover.xhtml">Cover</a></li>
		<li><a epub:type="titlepage" href="copyright.xhtml#title">Title Page</a></li>
		<li><a epub:type="toc" href="toc.xhtml#TOC">Table of Contents</a></li>
		<li><a epub:type="bodymatter" href="chapter1.xhtml">Start of Content</a></li>
	</ol>
</nav>



Images
If an image is important to the publication, but not required to be read at the point of insertion (i.e., it is not part of the logical reading order), use a figure tag to enclose it.
The background-image property remains largely unsupported because of the reflowable nature of ePUBs.
Bind captions to the corresponding image by using a wrapper around both.
HTML: Ensure consistent sizing with a SVG wrapper around the image tag. 
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="100%" height="100%" viewBox="0 0 573 800" preserveAspectRatio="xMidYMid meet">
   <img width="573" height="800" xlink:href="../images/img0032.png" />
	<p class=”caption”>....</p>
</svg>
CSS: Make image size responsive
img {
     max-width: 100%;
     oeb-column-number: 1;
     display: inline-block;
vertical-align: text-top;
}
.noresize {
    width: auto;
    display: block;
} 
.centered-art {
     font-style: normal;
     font-weight: normal;
     text-align: center;
     margin: 1em 0;
     text-indent: 0;
}
CSS: Remove page breaks from SVG and image elements.
svg, img {
page-break-inside: avoid;
}
Videos
Set video dimensions to avoid default rendering at 300 px by 150 px viewing area. 
Setting the max-width property to 100% is recommended to ensure that the video properly scales down to the available viewing area.
CSS
video#vid01 {
   width: 640px;
   height: 360px;
   max-width: 100%;
}
HTML
<video id="vid01" ... width="640" height="360">

Text
Avoid setting text color. Black text can disappear completely in the night-reading mode available on some devices.

CSS: Declare sans-serif font
font-family: Tahoma, Arial, Helvetica, "Microsoft YaHei New", "Microsoft Yahei", "微软雅黑", 宋体, SimSun, STXihei, "华文细黑", sans-serif;

CSS: Declare serif font
font-family: Georgia, "Times New Roman", "KaiTi", "楷体", STKaiti, "华文楷体", serif;

CSS: Remove page breaks on multiple line headings
h1, h2, h3, h4, h5, h6 {
   page-break-inside: avoid;
   page-break-after: avoid;
}
CSS: Remove all hyphenation (see below)
CSS: Setting widows and orphans to 1 effectively turns those features off overriding the default in some readers. (see below)
body {
   widows: 2;
   orphans: 2;
   margin: 0;
   text-indent: 0; /* This .Mobi7 hack is needed because that format automatically applies paragraph indents on all p classes */

   -webkit-line-break: after-white-space;
   -epub-line-break: strict;
   line-break: strict;

   -epub-word-break: keep-all !important;
   -webkit-word-break: keep-all !important;
   -moz-word-break: keep-all !important;
   word-break: keep-all !important;

   -webkit-hyphenate-lines: 0;
   hyphenate-lines: 0;

   -epub-hyphens: none !important;
   -webkit-hyphens: none !important;
   adobe-hyphenate: none !important;
   -moz-hyphens: none !important;
   hyphens: none !important;
}

CSS: Reset first paragraph indentation
p.first, h1+p, h2+p { 
    text-indent: 0;
} 

CSS: Create special wrapper to keep target text together on some when needed: 
div.keeptext {
     page-break-inside: avoid;
     margin: 0 !important;
}
CSS: Create span class to wrap around other tags in XHTML to fix Apple/iBooks bug regarding centered text
span.applebug {}
