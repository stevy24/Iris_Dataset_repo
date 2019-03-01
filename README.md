<!DOCTYPE html>
<!-- saved from url=(0109)http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb -->
<html lang="fr-fr"><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    

    <title>Iris_Dataset_Project</title>
    
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <link rel="stylesheet" href="./README_files/jquery-ui.min.css" type="text/css">
    <link rel="stylesheet" href="./README_files/jquery.typeahead.min.css" type="text/css">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    


<script type="text/javascript" src="./README_files/MathJax.js.download" charset="utf-8"></script>

<script type="text/javascript">
// MathJax disabled, set as null to distingish from *missing* MathJax,
// where it will be undefined, and should prompt a dialog later.
window.mathjax_url = "/static/components/MathJax/MathJax.js";
</script>

<link rel="stylesheet" href="./README_files/bootstrap-tour.min.css" type="text/css">
<link rel="stylesheet" href="./README_files/codemirror.css">


    <link rel="stylesheet" href="./README_files/style.min.css" type="text/css">
    

<link rel="stylesheet" href="./README_files/override.css" type="text/css">
<link rel="stylesheet" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb" id="kernel-css" type="text/css">


    <link rel="stylesheet" href="./README_files/custom.css" type="text/css">
    <script src="./README_files/promise.min.js.download" type="text/javascript" charset="utf-8"></script>
    <script src="./README_files/index.js.download" type="text/javascript"></script>
    <script src="./README_files/index.js(1).download" type="text/javascript"></script>
    <script src="./README_files/index.js(2).download" type="text/javascript"></script>
    <script src="./README_files/require.js.download" type="text/javascript" charset="utf-8"></script>
    <script>
      require.config({
          
          urlArgs: "v=20190301082907",
          
          baseUrl: '/static/',
          paths: {
            'auth/js/main': 'auth/js/main.min',
            custom : '/custom',
            nbextensions : '/nbextensions',
            kernelspecs : '/kernelspecs',
            underscore : 'components/underscore/underscore-min',
            backbone : 'components/backbone/backbone-min',
            jed: 'components/jed/jed',
            jquery: 'components/jquery/jquery.min',
            json: 'components/requirejs-plugins/src/json',
            text: 'components/requirejs-text/text',
            bootstrap: 'components/bootstrap/js/bootstrap.min',
            bootstraptour: 'components/bootstrap-tour/build/js/bootstrap-tour.min',
            'jquery-ui': 'components/jquery-ui/ui/minified/jquery-ui.min',
            moment: 'components/moment/min/moment-with-locales',
            codemirror: 'components/codemirror',
            termjs: 'components/xterm.js/xterm',
            typeahead: 'components/jquery-typeahead/dist/jquery.typeahead.min',
          },
          map: { // for backward compatibility
              "*": {
                  "jqueryui": "jquery-ui",
              }
          },
          shim: {
            typeahead: {
              deps: ["jquery"],
              exports: "typeahead"
            },
            underscore: {
              exports: '_'
            },
            backbone: {
              deps: ["underscore", "jquery"],
              exports: "Backbone"
            },
            bootstrap: {
              deps: ["jquery"],
              exports: "bootstrap"
            },
            bootstraptour: {
              deps: ["bootstrap"],
              exports: "Tour"
            },
            "jquery-ui": {
              deps: ["jquery"],
              exports: "$"
            }
          },
          waitSeconds: 30,
      });

      require.config({
          map: {
              '*':{
                'contents': 'services/contents',
              }
          }
      });

      // error-catching custom.js shim.
      define("custom", function (require, exports, module) {
          try {
              var custom = require('custom/custom');
              console.debug('loaded custom.js');
              return custom;
          } catch (e) {
              console.error("error loading custom.js", e);
              return {};
          }
      })

    document.nbjs_translations = {"domain": "nbjs", "locale_data": {"nbjs": {"": {"domain": "nbjs"}}}};
    document.documentElement.lang = navigator.language.toLowerCase();
    </script>

    
    

<script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="services/contents" src="./README_files/contents.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="custom/custom" src="./README_files/custom.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/plotlywidget/extension" src="./README_files/extension.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/jupyter-js-widgets/extension" src="./README_files/extension.js(1).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/nbextensions_configurator/config_menu/main" src="./README_files/main.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/contrib_nbextensions_help_item/main" src="./README_files/main.js(1).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/varInspector/main" src="./README_files/main.js(2).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/code_prettify" src="./README_files/code_prettify.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/collapsible_headings/main" src="./README_files/main.js(3).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/toc2/main" src="./README_files/main.js(4).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/main" src="./README_files/main.js(5).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/export_embedded/main" src="./README_files/main.js(6).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/autopep8" src="./README_files/autopep8.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_font_size/code_font_size" src="./README_files/code_font_size.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/gist_it/main" src="./README_files/main.js(7).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/python-markdown/main" src="./README_files/main.js(8).download"></script><style type="text/css">.MathJax_Hover_Frame {border-radius: .25em; -webkit-border-radius: .25em; -moz-border-radius: .25em; -khtml-border-radius: .25em; box-shadow: 0px 0px 15px #83A; -webkit-box-shadow: 0px 0px 15px #83A; -moz-box-shadow: 0px 0px 15px #83A; -khtml-box-shadow: 0px 0px 15px #83A; border: 1px solid #A6D ! important; display: inline-block; position: absolute}
.MathJax_Menu_Button .MathJax_Hover_Arrow {position: absolute; cursor: pointer; display: inline-block; border: 2px solid #AAA; border-radius: 4px; -webkit-border-radius: 4px; -moz-border-radius: 4px; -khtml-border-radius: 4px; font-family: 'Courier New',Courier; font-size: 9px; color: #F0F0F0}
.MathJax_Menu_Button .MathJax_Hover_Arrow span {display: block; background-color: #AAA; border: 1px solid; border-radius: 3px; line-height: 0; padding: 4px}
.MathJax_Hover_Arrow:hover {color: white!important; border: 2px solid #CCC!important}
.MathJax_Hover_Arrow:hover span {background-color: #CCC!important}
</style><style type="text/css">#MathJax_About {position: fixed; left: 50%; width: auto; text-align: center; border: 3px outset; padding: 1em 2em; background-color: #DDDDDD; color: black; cursor: default; font-family: message-box; font-size: 120%; font-style: normal; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; z-index: 201; border-radius: 15px; -webkit-border-radius: 15px; -moz-border-radius: 15px; -khtml-border-radius: 15px; box-shadow: 0px 10px 20px #808080; -webkit-box-shadow: 0px 10px 20px #808080; -moz-box-shadow: 0px 10px 20px #808080; -khtml-box-shadow: 0px 10px 20px #808080; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
#MathJax_About.MathJax_MousePost {outline: none}
.MathJax_Menu {position: absolute; background-color: white; color: black; width: auto; padding: 2px; border: 1px solid #CCCCCC; margin: 0; cursor: default; font: menu; text-align: left; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; z-index: 201; box-shadow: 0px 10px 20px #808080; -webkit-box-shadow: 0px 10px 20px #808080; -moz-box-shadow: 0px 10px 20px #808080; -khtml-box-shadow: 0px 10px 20px #808080; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
.MathJax_MenuItem {padding: 2px 2em; background: transparent}
.MathJax_MenuArrow {position: absolute; right: .5em; padding-top: .25em; color: #666666; font-size: .75em}
.MathJax_MenuActive .MathJax_MenuArrow {color: white}
.MathJax_MenuArrow.RTL {left: .5em; right: auto}
.MathJax_MenuCheck {position: absolute; left: .7em}
.MathJax_MenuCheck.RTL {right: .7em; left: auto}
.MathJax_MenuRadioCheck {position: absolute; left: 1em}
.MathJax_MenuRadioCheck.RTL {right: 1em; left: auto}
.MathJax_MenuLabel {padding: 2px 2em 4px 1.33em; font-style: italic}
.MathJax_MenuRule {border-top: 1px solid #CCCCCC; margin: 4px 1px 0px}
.MathJax_MenuDisabled {color: GrayText}
.MathJax_MenuActive {background-color: Highlight; color: HighlightText}
.MathJax_MenuDisabled:focus, .MathJax_MenuLabel:focus {background-color: #E8E8E8}
.MathJax_ContextMenu:focus {outline: none}
.MathJax_ContextMenu .MathJax_MenuItem:focus {outline: none}
#MathJax_AboutClose {top: .2em; right: .2em}
.MathJax_Menu .MathJax_MenuClose {top: -10px; left: -10px}
.MathJax_MenuClose {position: absolute; cursor: pointer; display: inline-block; border: 2px solid #AAA; border-radius: 18px; -webkit-border-radius: 18px; -moz-border-radius: 18px; -khtml-border-radius: 18px; font-family: 'Courier New',Courier; font-size: 24px; color: #F0F0F0}
.MathJax_MenuClose span {display: block; background-color: #AAA; border: 1.5px solid; border-radius: 18px; -webkit-border-radius: 18px; -moz-border-radius: 18px; -khtml-border-radius: 18px; line-height: 0; padding: 8px 0 6px}
.MathJax_MenuClose:hover {color: white!important; border: 2px solid #CCC!important}
.MathJax_MenuClose:hover span {background-color: #CCC!important}
.MathJax_MenuClose:hover:focus {outline: none}
</style><style type="text/css">.MathJax_Preview .MJXf-math {color: inherit!important}
</style><style type="text/css">.MJX_Assistive_MathML {position: absolute!important; top: 0; left: 0; clip: rect(1px, 1px, 1px, 1px); padding: 1px 0 0 0!important; border: 0!important; height: 1px!important; width: 1px!important; overflow: hidden!important; display: block!important; -webkit-touch-callout: none; -webkit-user-select: none; -khtml-user-select: none; -moz-user-select: none; -ms-user-select: none; user-select: none}
.MJX_Assistive_MathML.MJX_Assistive_MathML_Block {width: 100%!important}
</style><style type="text/css">#MathJax_Zoom {position: absolute; background-color: #F0F0F0; overflow: auto; display: block; z-index: 301; padding: .5em; border: 1px solid black; margin: 0; font-weight: normal; font-style: normal; text-align: left; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; -webkit-box-sizing: content-box; -moz-box-sizing: content-box; box-sizing: content-box; box-shadow: 5px 5px 15px #AAAAAA; -webkit-box-shadow: 5px 5px 15px #AAAAAA; -moz-box-shadow: 5px 5px 15px #AAAAAA; -khtml-box-shadow: 5px 5px 15px #AAAAAA; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
#MathJax_ZoomOverlay {position: absolute; left: 0; top: 0; z-index: 300; display: inline-block; width: 100%; height: 100%; border: 0; padding: 0; margin: 0; background-color: white; opacity: 0; filter: alpha(opacity=0)}
#MathJax_ZoomFrame {position: relative; display: inline-block; height: 0; width: 0}
#MathJax_ZoomEventTrap {position: absolute; left: 0; top: 0; z-index: 302; display: inline-block; border: 0; padding: 0; margin: 0; background-color: white; opacity: 0; filter: alpha(opacity=0)}
</style><style type="text/css">.MathJax_Preview {color: #888}
#MathJax_Message {position: fixed; left: 1em; bottom: 1.5em; background-color: #E6E6E6; border: 1px solid #959595; margin: 0px; padding: 2px 8px; z-index: 102; color: black; font-size: 80%; width: auto; white-space: nowrap}
#MathJax_MSIE_Frame {position: absolute; top: 0; left: 0; width: 0px; z-index: 101; border: 0px; margin: 0px; padding: 0px}
.MathJax_Error {color: #CC0000; font-style: italic}
</style><link type="text/css" rel="stylesheet" href="./README_files/main.css"><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/kernel_exec_on_cell" src="./README_files/kernel_exec_on_cell.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/toc2/toc2" src="./README_files/toc2.js.download"></script><link id="collapsible_headings_css" rel="stylesheet" type="text/css" href="./README_files/main(1).css"><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/foldcode" src="./README_files/foldcode.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/foldgutter" src="./README_files/foldgutter.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/brace-fold" src="./README_files/brace-fold.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/indent-fold" src="./README_files/indent-fold.js.download"></script><link type="text/css" rel="stylesheet" href="./README_files/main(2).css"><style type="text/css">div.MathJax_MathML {text-align: center; margin: .75em 0px; display: block!important}
.MathJax_MathML {font-style: normal; font-weight: normal; line-height: normal; font-size: 100%; font-size-adjust: none; text-indent: 0; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0; min-height: 0; border: 0; padding: 0; margin: 0}
span.MathJax_MathML {display: inline!important}
.MathJax_mmlExBox {display: block!important; overflow: hidden; height: 1px; width: 60ex; min-height: 0; max-height: none; padding: 0; border: 0; margin: 0}
[class="MJX-tex-oldstyle"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB}
[class="MJX-tex-oldstyle-bold"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB; font-weight: bold}
[class="MJX-tex-caligraphic"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB}
[class="MJX-tex-caligraphic-bold"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB; font-weight: bold}
@font-face /*1*/ {font-family: MathJax_Caligraphic-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Caligraphic-Regular.otf')}
@font-face /*2*/ {font-family: MathJax_Caligraphic-WEB; font-weight: bold; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Caligraphic-Bold.otf')}
[mathvariant="double-struck"] {font-family: MathJax_AMS, MathJax_AMS-WEB}
[mathvariant="script"] {font-family: MathJax_Script, MathJax_Script-WEB}
[mathvariant="fraktur"] {font-family: MathJax_Fraktur, MathJax_Fraktur-WEB}
[mathvariant="bold-script"] {font-family: MathJax_Script, MathJax_Caligraphic-WEB; font-weight: bold}
[mathvariant="bold-fraktur"] {font-family: MathJax_Fraktur, MathJax_Fraktur-WEB; font-weight: bold}
[mathvariant="monospace"] {font-family: monospace}
[mathvariant="sans-serif"] {font-family: sans-serif}
[mathvariant="bold-sans-serif"] {font-family: sans-serif; font-weight: bold}
[mathvariant="sans-serif-italic"] {font-family: sans-serif; font-style: italic}
[mathvariant="sans-serif-bold-italic"] {font-family: sans-serif; font-style: italic; font-weight: bold}
@font-face /*3*/ {font-family: MathJax_AMS-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_AMS-Regular.otf')}
@font-face /*4*/ {font-family: MathJax_Script-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Script-Regular.otf')}
@font-face /*5*/ {font-family: MathJax_Fraktur-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Fraktur-Regular.otf')}
@font-face /*6*/ {font-family: MathJax_Fraktur-WEB; font-weight: bold; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Fraktur-Bold.otf')}
</style><style type="text/css">.MJXp-script {font-size: .8em}
.MJXp-right {-webkit-transform-origin: right; -moz-transform-origin: right; -ms-transform-origin: right; -o-transform-origin: right; transform-origin: right}
.MJXp-bold {font-weight: bold}
.MJXp-italic {font-style: italic}
.MJXp-scr {font-family: MathJax_Script,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-frak {font-family: MathJax_Fraktur,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-sf {font-family: MathJax_SansSerif,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-cal {font-family: MathJax_Caligraphic,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-mono {font-family: MathJax_Typewriter,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-largeop {font-size: 150%}
.MJXp-largeop.MJXp-int {vertical-align: -.2em}
.MJXp-math {display: inline-block; line-height: 1.2; text-indent: 0; font-family: 'Times New Roman',Times,STIXGeneral,serif; white-space: nowrap; border-collapse: collapse}
.MJXp-display {display: block; text-align: center; margin: 1em 0}
.MJXp-math span {display: inline-block}
.MJXp-box {display: block!important; text-align: center}
.MJXp-box:after {content: " "}
.MJXp-rule {display: block!important; margin-top: .1em}
.MJXp-char {display: block!important}
.MJXp-mo {margin: 0 .15em}
.MJXp-mfrac {margin: 0 .125em; vertical-align: .25em}
.MJXp-denom {display: inline-table!important; width: 100%}
.MJXp-denom > * {display: table-row!important}
.MJXp-surd {vertical-align: top}
.MJXp-surd > * {display: block!important}
.MJXp-script-box > *  {display: table!important; height: 50%}
.MJXp-script-box > * > * {display: table-cell!important; vertical-align: top}
.MJXp-script-box > *:last-child > * {vertical-align: bottom}
.MJXp-script-box > * > * > * {display: block!important}
.MJXp-mphantom {visibility: hidden}
.MJXp-munderover {display: inline-table!important}
.MJXp-over {display: inline-block!important; text-align: center}
.MJXp-over > * {display: block!important}
.MJXp-munderover > * {display: table-row!important}
.MJXp-mtable {vertical-align: .25em; margin: 0 .125em}
.MJXp-mtable > * {display: inline-table!important; vertical-align: middle}
.MJXp-mtr {display: table-row!important}
.MJXp-mtd {display: table-cell!important; text-align: center; padding: .5em 0 0 .5em}
.MJXp-mtr > .MJXp-mtd:first-child {padding-left: 0}
.MJXp-mtr:first-child > .MJXp-mtd {padding-top: 0}
.MJXp-mlabeledtr {display: table-row!important}
.MJXp-mlabeledtr > .MJXp-mtd:first-child {padding-left: 0}
.MJXp-mlabeledtr:first-child > .MJXp-mtd {padding-top: 0}
.MJXp-merror {background-color: #FFFF88; color: #CC0000; border: 1px solid #CC0000; padding: 1px 3px; font-style: normal; font-size: 90%}
.MJXp-scale0 {-webkit-transform: scaleX(.0); -moz-transform: scaleX(.0); -ms-transform: scaleX(.0); -o-transform: scaleX(.0); transform: scaleX(.0)}
.MJXp-scale1 {-webkit-transform: scaleX(.1); -moz-transform: scaleX(.1); -ms-transform: scaleX(.1); -o-transform: scaleX(.1); transform: scaleX(.1)}
.MJXp-scale2 {-webkit-transform: scaleX(.2); -moz-transform: scaleX(.2); -ms-transform: scaleX(.2); -o-transform: scaleX(.2); transform: scaleX(.2)}
.MJXp-scale3 {-webkit-transform: scaleX(.3); -moz-transform: scaleX(.3); -ms-transform: scaleX(.3); -o-transform: scaleX(.3); transform: scaleX(.3)}
.MJXp-scale4 {-webkit-transform: scaleX(.4); -moz-transform: scaleX(.4); -ms-transform: scaleX(.4); -o-transform: scaleX(.4); transform: scaleX(.4)}
.MJXp-scale5 {-webkit-transform: scaleX(.5); -moz-transform: scaleX(.5); -ms-transform: scaleX(.5); -o-transform: scaleX(.5); transform: scaleX(.5)}
.MJXp-scale6 {-webkit-transform: scaleX(.6); -moz-transform: scaleX(.6); -ms-transform: scaleX(.6); -o-transform: scaleX(.6); transform: scaleX(.6)}
.MJXp-scale7 {-webkit-transform: scaleX(.7); -moz-transform: scaleX(.7); -ms-transform: scaleX(.7); -o-transform: scaleX(.7); transform: scaleX(.7)}
.MJXp-scale8 {-webkit-transform: scaleX(.8); -moz-transform: scaleX(.8); -ms-transform: scaleX(.8); -o-transform: scaleX(.8); transform: scaleX(.8)}
.MJXp-scale9 {-webkit-transform: scaleX(.9); -moz-transform: scaleX(.9); -ms-transform: scaleX(.9); -o-transform: scaleX(.9); transform: scaleX(.9)}
.MathJax_PHTML .noError {vertical-align: ; font-size: 90%; text-align: left; color: black; padding: 1px 3px; border: 1px solid}
</style><style id="collapsible_headings_indent_css">.collapsible_headings_toggle .h1 { margin-right: 40px; }
.collapsible_headings_toggle .h2 { margin-right: 32px; }
.collapsible_headings_toggle .h3 { margin-right: 24px; }
.collapsible_headings_toggle .h4 { margin-right: 16px; }
.collapsible_headings_toggle .h5 { margin-right: 8px; }
.collapsible_headings_toggle .h6 { margin-right: 0px; }</style><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/varInspector/jquery.tablesorter.min" src="./README_files/jquery.tablesorter.min.js.download"></script><style type="text/css">/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/* Override the correction for the prompt area in https://github.com/jupyter/notebook/blob/dd41d9fd5c4f698bd7468612d877828a7eeb0e7a/IPython/html/static/notebook/less/outputarea.less#L110 */

.jupyter-widgets-output-area div.output_subarea {
    max-width: 100%;
}

/* Work-around for the bug fixed in https://github.com/jupyter/notebook/pull/2961 */

.jupyter-widgets-output-area > .out_prompt_overlay {
    display: none;
}
</style><style type="text/css">.MathJax_Display {text-align: center; margin: 0; position: relative; display: block!important; text-indent: 0; max-width: none; max-height: none; min-width: 0; min-height: 0; width: 100%}
.MathJax .merror {background-color: #FFFF88; color: #CC0000; border: 1px solid #CC0000; padding: 1px 3px; font-style: normal; font-size: 90%}
.MathJax .MJX-monospace {font-family: monospace}
.MathJax .MJX-sans-serif {font-family: sans-serif}
#MathJax_Tooltip {background-color: InfoBackground; color: InfoText; border: 1px solid black; box-shadow: 2px 2px 5px #AAAAAA; -webkit-box-shadow: 2px 2px 5px #AAAAAA; -moz-box-shadow: 2px 2px 5px #AAAAAA; -khtml-box-shadow: 2px 2px 5px #AAAAAA; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true'); padding: 3px 4px; z-index: 401; position: absolute; left: 0; top: 0; width: auto; height: auto; display: none}
.MathJax {display: inline; font-style: normal; font-weight: normal; line-height: normal; font-size: 100%; font-size-adjust: none; text-indent: 0; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0; min-height: 0; border: 0; padding: 0; margin: 0}
.MathJax:focus, body :focus .MathJax {display: inline-table}
.MathJax.MathJax_FullWidth {text-align: center; display: table-cell!important; width: 10000em!important}
.MathJax img, .MathJax nobr, .MathJax a {border: 0; padding: 0; margin: 0; max-width: none; max-height: none; min-width: 0; min-height: 0; vertical-align: 0; line-height: normal; text-decoration: none}
img.MathJax_strut {border: 0!important; padding: 0!important; margin: 0!important; vertical-align: 0!important}
.MathJax span {display: inline; position: static; border: 0; padding: 0; margin: 0; vertical-align: 0; line-height: normal; text-decoration: none; box-sizing: content-box}
.MathJax nobr {white-space: nowrap!important}
.MathJax img {display: inline!important; float: none!important}
.MathJax * {transition: none; -webkit-transition: none; -moz-transition: none; -ms-transition: none; -o-transition: none}
.MathJax_Processing {visibility: hidden; position: fixed; width: 0; height: 0; overflow: hidden}
.MathJax_Processed {display: none!important}
.MathJax_ExBox {display: block!important; overflow: hidden; width: 1px; height: 60ex; min-height: 0; max-height: none}
.MathJax .MathJax_EmBox {display: block!important; overflow: hidden; width: 1px; height: 60em; min-height: 0; max-height: none}
.MathJax_LineBox {display: table!important}
.MathJax_LineBox span {display: table-cell!important; width: 10000em!important; min-width: 0; max-width: none; padding: 0; border: 0; margin: 0}
.MathJax .MathJax_HitBox {cursor: text; background: white; opacity: 0; filter: alpha(opacity=0)}
.MathJax .MathJax_HitBox * {filter: none; opacity: 1; background: transparent}
#MathJax_Tooltip * {filter: none; opacity: 1; background: transparent}
@font-face {font-family: MathJax_Blank; src: url('about:blank')}
.MathJax .noError {vertical-align: ; font-size: 90%; text-align: left; color: black; padding: 1px 3px; border: 1px solid}
</style><link type="text/css" rel="stylesheet" href="./README_files/main(3).css"><link type="text/css" rel="stylesheet" href="./README_files/foldgutter.css"><link type="text/css" rel="stylesheet" href="./README_files/foldgutter(1).css"><style type="text/css">/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-Widget {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: relative;
  overflow: hidden;
  cursor: default;
}
.p-Widget.p-mod-hidden {
  display: none !important;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-CommandPalette {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-CommandPalette-search {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-content {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}
.p-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.p-CommandPalette-item {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-CommandPalette-itemIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-itemContent {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
}
.p-CommandPalette-itemShortcut {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-DockPanel {
  z-index: 0;
}
.p-DockPanel-widget {
  z-index: 0;
}
.p-DockPanel-tabBar {
  z-index: 1;
}
.p-DockPanel-handle {
  z-index: 2;
}
.p-DockPanel-handle.p-mod-hidden {
  display: none !important;
}
.p-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}
.p-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}
.p-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}
.p-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  -webkit-transform: translateX(-50%);
          transform: translateX(-50%);
}
.p-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  -webkit-transform: translateY(-50%);
          transform: translateY(-50%);
}
.p-DockPanel-overlay {
  z-index: 3;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  pointer-events: none;
}
.p-DockPanel-overlay.p-mod-hidden {
  display: none !important;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}
.p-Menu-item {
  display: table-row;
}
.p-Menu-item.p-mod-hidden,
.p-Menu-item.p-mod-collapsed {
  display: none !important;
}
.p-Menu-itemIcon,
.p-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}
.p-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}
.p-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-MenuBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  list-style-type: none;
}
.p-MenuBar-item {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
}
.p-MenuBar-itemIcon,
.p-MenuBar-itemLabel {
  display: inline-block;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-ScrollBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-ScrollBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-ScrollBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-ScrollBar-button {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-ScrollBar-track {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: relative;
  overflow: hidden;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
}
.p-ScrollBar-thumb {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: absolute;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-SplitPanel-child {
  z-index: 0;
}
.p-SplitPanel-handle {
  z-index: 1;
}
.p-SplitPanel-handle.p-mod-hidden {
  display: none !important;
}
.p-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle {
  cursor: ew-resize;
}
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle {
  cursor: ns-resize;
}
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  -webkit-transform: translateX(-50%);
          transform: translateX(-50%);
}
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  -webkit-transform: translateY(-50%);
          transform: translateY(-50%);
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-TabBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-TabBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-TabBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-TabBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  list-style-type: none;
}
.p-TabBar[data-orientation='horizontal'] > .p-TabBar-content {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-TabBar[data-orientation='vertical'] > .p-TabBar-content {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-TabBar-tab {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  overflow: hidden;
}
.p-TabBar-tabIcon,
.p-TabBar-tabCloseIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-TabBar-tabLabel {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}
.p-TabBar-tab.p-mod-hidden {
  display: none !important;
}
.p-TabBar.p-mod-dragging .p-TabBar-tab {
  position: relative;
}
.p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab {
  left: 0;
  -webkit-transition: left 150ms ease;
  transition: left 150ms ease;
}
.p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab {
  top: 0;
  -webkit-transition: top 150ms ease;
  transition: top 150ms ease;
}
.p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging {
  -webkit-transition: none;
  transition: none;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-TabPanel-tabBar {
  z-index: 1;
}
.p-TabPanel-stackedPanel {
  z-index: 0;
}
</style><style type="text/css">/* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 .jupyter-widgets-disconnected::before {
    content: "\F127"; /* chain-broken */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #d9534f;
    padding: 3px;
    -ms-flex-item-align: start;
        align-self: flex-start;
}
</style><style type="text/css">/* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 /* We import all of these together in a single css file because the Webpack
loader sees only one file at a time. This allows postcss to see the variable
definitions when they are used. */

 /*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

 /*
This file is copied from the JupyterLab project to define default styling for
when the widget styling is compiled down to eliminate CSS variables. We make one
change - we comment out the font import below.
*/

 /**
 * The material design colors are adapted from google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 * https://github.com/danlevan/google-material-color/blob/f67ca5f4028b2f1b34862f64b0ca67323f91b088/dist/palette.var.css
 *
 * The license for the material design color CSS variables is as follows (see
 * https://github.com/danlevan/google-material-color/blob/f67ca5f4028b2f1b34862f64b0ca67323f91b088/LICENSE)
 *
 * The MIT License (MIT)
 *
 * Copyright (c) 2014 Dan Le Van
 *
 * Permission is hereby granted, free of charge, to any person obtaining a copy
 * of this software and associated documentation files (the "Software"), to deal
 * in the Software without restriction, including without limitation the rights
 * to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 * copies of the Software, and to permit persons to whom the Software is
 * furnished to do so, subject to the following conditions:
 *
 * The above copyright notice and this permission notice shall be included in
 * all copies or substantial portions of the Software.
 *
 * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 * IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 * FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 * AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 * LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 * OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 * SOFTWARE.
 */

 /*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

 /*
 * Optional monospace font for input/output prompt.
 */

 /* Commented out in ipywidgets since we don't need it. */

 /* @import url('https://fonts.googleapis.com/css?family=Roboto+Mono'); */

 /*
 * Added for compabitility with output area
 */

 :root {

  /* Borders

  The following variables, specify the visual styling of borders in JupyterLab.
   */

  /* UI Fonts

  The UI font CSS variables are used for the typography all of the JupyterLab
  user interface elements that are not directly user generated content.
  */ /* Base font size */ /* Ensures px perfect FontAwesome icons */

  /* Use these font colors against the corresponding main layout colors.
     In a light theme, these go from dark to light.
  */

  /* Use these against the brand/accent/warn/error colors.
     These will typically go from light to darker, in both a dark and light theme
   */

  /* Content Fonts

  Content font variables are used for typography of user generated content.
  */ /* Base font size */


  /* Layout

  The following are the main layout colors use in JupyterLab. In a light
  theme these would go from light to dark.
  */

  /* Brand/accent */

  /* State colors (warn, error, success, info) */

  /* Cell specific styles */
  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */

  /* Notebook specific styles */

  /* Console specific styles */

  /* Toolbar specific styles */
}

 /* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 /*
 * We assume that the CSS variables in
 * https://github.com/jupyterlab/jupyterlab/blob/master/src/default-theme/variables.css
 * have been defined.
 */

 /* This file has code derived from PhosphorJS CSS files, as noted below. The license for this PhosphorJS code is:

Copyright (c) 2014-2017, PhosphorJS Contributors
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

* Neither the name of the copyright holder nor the names of its
  contributors may be used to endorse or promote products derived from
  this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

*/

 /*
 * The following section is derived from https://github.com/phosphorjs/phosphor/blob/23b9d075ebc5b73ab148b6ebfc20af97f85714c4/packages/widgets/style/tabbar.css 
 * We've scoped the rules so that they are consistent with exactly our code.
 */

 .jupyter-widgets.widget-tab > .p-TabBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar > .p-TabBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  list-style-type: none;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='horizontal'] > .p-TabBar-content {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='vertical'] > .p-TabBar-content {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  overflow: hidden;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabIcon,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabCloseIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabLabel {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-hidden {
  display: none !important;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging .p-TabBar-tab {
  position: relative;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab {
  left: 0;
  -webkit-transition: left 150ms ease;
  transition: left 150ms ease;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab {
  top: 0;
  -webkit-transition: top 150ms ease;
  transition: top 150ms ease;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging {
  -webkit-transition: none;
  transition: none;
}

 /* End tabbar.css */

 :root { /* margin between inline elements */

    /* From Material Design Lite */
}

 .jupyter-widgets {
    margin: 2px;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    color: black;
    overflow: visible;
}

 .jupyter-widgets.jupyter-widgets-disconnected::before {
    line-height: 28px;
    height: 28px;
}

 .jp-Output-result > .jupyter-widgets {
    margin-left: 0;
    margin-right: 0;
}

 /* vbox and hbox */

 .widget-inline-hbox {
    /* Horizontal widgets */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
    -webkit-box-align: baseline;
        -ms-flex-align: baseline;
            align-items: baseline;
}

 .widget-inline-vbox {
    /* Vertical Widgets */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
}

 .widget-box {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    margin: 0;
    overflow: auto;
}

 .widget-gridbox {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: grid;
    margin: 0;
    overflow: auto;
}

 .widget-hbox {
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
}

 .widget-vbox {
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 /* General Button Styling */

 .jupyter-button {
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 0px;
    padding-bottom: 0px;
    display: inline-block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: center;
    font-size: 13px;
    cursor: pointer;

    height: 28px;
    border: 0px solid;
    line-height: 28px;
    -webkit-box-shadow: none;
            box-shadow: none;

    color: rgba(0, 0, 0, .8);
    background-color: #EEEEEE;
    border-color: #E0E0E0;
    border: none;
}

 .jupyter-button i.fa {
    margin-right: 4px;
    pointer-events: none;
}

 .jupyter-button:empty:before {
    content: "\200B"; /* zero-width space */
}

 .jupyter-widgets.jupyter-button:disabled {
    opacity: 0.6;
}

 .jupyter-button i.fa.center {
    margin-right: 0;
}

 .jupyter-button:hover:enabled, .jupyter-button:focus:enabled {
    /* MD Lite 2dp shadow */
    -webkit-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .14),
                0 3px 1px -2px rgba(0, 0, 0, .2),
                0 1px 5px 0 rgba(0, 0, 0, .12);
            box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .14),
                0 3px 1px -2px rgba(0, 0, 0, .2),
                0 1px 5px 0 rgba(0, 0, 0, .12);
}

 .jupyter-button:active, .jupyter-button.mod-active {
    /* MD Lite 4dp shadow */
    -webkit-box-shadow: 0 4px 5px 0 rgba(0, 0, 0, .14),
                0 1px 10px 0 rgba(0, 0, 0, .12),
                0 2px 4px -1px rgba(0, 0, 0, .2);
            box-shadow: 0 4px 5px 0 rgba(0, 0, 0, .14),
                0 1px 10px 0 rgba(0, 0, 0, .12),
                0 2px 4px -1px rgba(0, 0, 0, .2);
    color: rgba(0, 0, 0, .8);
    background-color: #BDBDBD;
}

 .jupyter-button:focus:enabled {
    outline: 1px solid #64B5F6;
}

 /* Button "Primary" Styling */

 .jupyter-button.mod-primary {
    color: rgba(255, 255, 255, 1.0);
    background-color: #2196F3;
}

 .jupyter-button.mod-primary.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #1976D2;
}

 .jupyter-button.mod-primary:active {
    color: rgba(255, 255, 255, 1);
    background-color: #1976D2;
}

 /* Button "Success" Styling */

 .jupyter-button.mod-success {
    color: rgba(255, 255, 255, 1.0);
    background-color: #4CAF50;
}

 .jupyter-button.mod-success.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #388E3C;
 }

 .jupyter-button.mod-success:active {
    color: rgba(255, 255, 255, 1);
    background-color: #388E3C;
 }

 /* Button "Info" Styling */

 .jupyter-button.mod-info {
    color: rgba(255, 255, 255, 1.0);
    background-color: #00BCD4;
}

 .jupyter-button.mod-info.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #0097A7;
}

 .jupyter-button.mod-info:active {
    color: rgba(255, 255, 255, 1);
    background-color: #0097A7;
}

 /* Button "Warning" Styling */

 .jupyter-button.mod-warning {
    color: rgba(255, 255, 255, 1.0);
    background-color: #FF9800;
}

 .jupyter-button.mod-warning.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #F57C00;
}

 .jupyter-button.mod-warning:active {
    color: rgba(255, 255, 255, 1);
    background-color: #F57C00;
}

 /* Button "Danger" Styling */

 .jupyter-button.mod-danger {
    color: rgba(255, 255, 255, 1.0);
    background-color: #F44336;
}

 .jupyter-button.mod-danger.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #D32F2F;
}

 .jupyter-button.mod-danger:active {
    color: rgba(255, 255, 255, 1);
    background-color: #D32F2F;
}

 /* Widget Button*/

 .widget-button, .widget-toggle-button {
    width: 148px;
}

 /* Widget Label Styling */

 /* Override Bootstrap label css */

 .jupyter-widgets label {
    margin-bottom: 0;
    margin-bottom: initial;
}

 .widget-label-basic {
    /* Basic Label */
    color: black;
    font-size: 13px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    line-height: 28px;
}

 .widget-label {
    /* Label */
    color: black;
    font-size: 13px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    line-height: 28px;
}

 .widget-inline-hbox .widget-label {
    /* Horizontal Widget Label */
    color: black;
    text-align: right;
    margin-right: 8px;
    width: 80px;
    -ms-flex-negative: 0;
        flex-shrink: 0;
}

 .widget-inline-vbox .widget-label {
    /* Vertical Widget Label */
    color: black;
    text-align: center;
    line-height: 28px;
}

 /* Widget Readout Styling */

 .widget-readout {
    color: black;
    font-size: 13px;
    height: 28px;
    line-height: 28px;
    overflow: hidden;
    white-space: nowrap;
    text-align: center;
}

 .widget-readout.overflow {
    /* Overflowing Readout */

    /* From Material Design Lite
        shadow-key-umbra-opacity: 0.2;
        shadow-key-penumbra-opacity: 0.14;
        shadow-ambient-shadow-opacity: 0.12;
     */
    -webkit-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .2),
                        0 3px 1px -2px rgba(0, 0, 0, .14),
                        0 1px 5px 0 rgba(0, 0, 0, .12);

    box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .2),
                0 3px 1px -2px rgba(0, 0, 0, .14),
                0 1px 5px 0 rgba(0, 0, 0, .12);
}

 .widget-inline-hbox .widget-readout {
    /* Horizontal Readout */
    text-align: center;
    max-width: 148px;
    min-width: 72px;
    margin-left: 4px;
}

 .widget-inline-vbox .widget-readout {
    /* Vertical Readout */
    margin-top: 4px;
    /* as wide as the widget */
    width: inherit;
}

 /* Widget Checkbox Styling */

 .widget-checkbox {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-checkbox input[type="checkbox"] {
    margin: 0px 8px 0px 0px;
    line-height: 28px;
    font-size: large;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 0;
        flex-shrink: 0;
    -ms-flex-item-align: center;
        align-self: center;
}

 /* Widget Valid Styling */

 .widget-valid {
    height: 28px;
    line-height: 28px;
    width: 148px;
    font-size: 13px;
}

 .widget-valid i:before {
    line-height: 28px;
    margin-right: 4px;
    margin-left: 4px;

    /* from the fa class in FontAwesome: https://github.com/FortAwesome/Font-Awesome/blob/49100c7c3a7b58d50baa71efef11af41a66b03d3/css/font-awesome.css#L14 */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

 .widget-valid.mod-valid i:before {
    content: "\F00C";
    color: green;
}

 .widget-valid.mod-invalid i:before {
    content: "\F00D";
    color: red;
}

 .widget-valid.mod-valid .widget-valid-readout {
    display: none;
}

 /* Widget Text and TextArea Stying */

 .widget-textarea, .widget-text {
    width: 300px;
}

 .widget-text input[type="text"], .widget-text input[type="number"]{
    height: 28px;
    line-height: 28px;
}

 .widget-text input[type="text"]:disabled, .widget-text input[type="number"]:disabled, .widget-textarea textarea:disabled {
    opacity: 0.6;
}

 .widget-text input[type="text"], .widget-text input[type="number"], .widget-textarea textarea {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    padding: 4px 8px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -ms-flex-negative: 1;
        flex-shrink: 1;
    outline: none !important;
}

 .widget-textarea textarea {
    height: inherit;
    width: inherit;
}

 .widget-text input:focus, .widget-textarea textarea:focus {
    border-color: #64B5F6;
}

 /* Widget Slider */

 .widget-slider .ui-slider {
    /* Slider Track */
    border: 1px solid #BDBDBD;
    background: #BDBDBD;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    position: relative;
    border-radius: 0px;
}

 .widget-slider .ui-slider .ui-slider-handle {
    /* Slider Handle */
    outline: none !important; /* focused slider handles are colored - see below */
    position: absolute;
    background-color: white;
    border: 1px solid #9E9E9E;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    z-index: 1;
    background-image: none; /* Override jquery-ui */
}

 /* Override jquery-ui */

 .widget-slider .ui-slider .ui-slider-handle:hover, .widget-slider .ui-slider .ui-slider-handle:focus {
    background-color: #2196F3;
    border: 1px solid #2196F3;
}

 .widget-slider .ui-slider .ui-slider-handle:active {
    background-color: #2196F3;
    border-color: #2196F3;
    z-index: 2;
    -webkit-transform: scale(1.2);
            transform: scale(1.2);
}

 .widget-slider  .ui-slider .ui-slider-range {
    /* Interval between the two specified value of a double slider */
    position: absolute;
    background: #2196F3;
    z-index: 0;
}

 /* Shapes of Slider Handles */

 .widget-hslider .ui-slider .ui-slider-handle {
    width: 16px;
    height: 16px;
    margin-top: -7px;
    margin-left: -7px;
    border-radius: 50%;
    top: 0;
}

 .widget-vslider .ui-slider .ui-slider-handle {
    width: 16px;
    height: 16px;
    margin-bottom: -7px;
    margin-left: -7px;
    border-radius: 50%;
    left: 0;
}

 .widget-hslider .ui-slider .ui-slider-range {
    height: 8px;
    margin-top: -3px;
}

 .widget-vslider .ui-slider .ui-slider-range {
    width: 8px;
    margin-left: -3px;
}

 /* Horizontal Slider */

 .widget-hslider {
    width: 300px;
    height: 28px;
    line-height: 28px;

    /* Override the align-items baseline. This way, the description and readout
    still seem to align their baseline properly, and we don't have to have
    align-self: stretch in the .slider-container. */
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
}

 .widgets-slider .slider-container {
    overflow: visible;
}

 .widget-hslider .slider-container {
    height: 28px;
    margin-left: 6px;
    margin-right: 6px;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
}

 .widget-hslider .ui-slider {
    /* Inner, invisible slide div */
    height: 4px;
    margin-top: 12px;
    width: 100%;
}

 /* Vertical Slider */

 .widget-vbox .widget-label {
    height: 28px;
    line-height: 28px;
}

 .widget-vslider {
    /* Vertical Slider */
    height: 200px;
    width: 72px;
}

 .widget-vslider .slider-container {
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 6px;
    margin-top: 6px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 .widget-vslider .ui-slider-vertical {
    /* Inner, invisible slide div */
    width: 4px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-left: auto;
    margin-right: auto;
}

 /* Widget Progress Styling */

 .progress-bar {
    -webkit-transition: none;
    transition: none;
}

 .progress-bar {
    height: 28px;
}

 .progress-bar {
    background-color: #2196F3;
}

 .progress-bar-success {
    background-color: #4CAF50;
}

 .progress-bar-info {
    background-color: #00BCD4;
}

 .progress-bar-warning {
    background-color: #FF9800;
}

 .progress-bar-danger {
    background-color: #F44336;
}

 .progress {
    background-color: #EEEEEE;
    border: none;
    -webkit-box-shadow: none;
            box-shadow: none;
}

 /* Horisontal Progress */

 .widget-hprogress {
    /* Progress Bar */
    height: 28px;
    line-height: 28px;
    width: 300px;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;

}

 .widget-hprogress .progress {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-top: 4px;
    margin-bottom: 4px;
    -ms-flex-item-align: stretch;
        align-self: stretch;
    /* Override bootstrap style */
    height: auto;
    height: initial;
}

 /* Vertical Progress */

 .widget-vprogress {
    height: 200px;
    width: 72px;
}

 .widget-vprogress .progress {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    width: 20px;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 0;
}

 /* Select Widget Styling */

 .widget-dropdown {
    height: 28px;
    width: 300px;
    line-height: 28px;
}

 .widget-dropdown > select {
    padding-right: 20px;
    border: 1px solid #9E9E9E;
    border-radius: 0;
    height: inherit;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    outline: none !important;
    -webkit-box-shadow: none;
            box-shadow: none;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    vertical-align: top;
    padding-left: 8px;
	appearance: none;
	-webkit-appearance: none;
	-moz-appearance: none;
    background-repeat: no-repeat;
	background-size: 20px;
	background-position: right center;
    background-image: url("data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDE5LjIuMSwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPgo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IgoJIHZpZXdCb3g9IjAgMCAxOCAxOCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMTggMTg7IiB4bWw6c3BhY2U9InByZXNlcnZlIj4KPHN0eWxlIHR5cGU9InRleHQvY3NzIj4KCS5zdDB7ZmlsbDpub25lO30KPC9zdHlsZT4KPHBhdGggZD0iTTUuMiw1LjlMOSw5LjdsMy44LTMuOGwxLjIsMS4ybC00LjksNWwtNC45LTVMNS4yLDUuOXoiLz4KPHBhdGggY2xhc3M9InN0MCIgZD0iTTAtMC42aDE4djE4SDBWLTAuNnoiLz4KPC9zdmc+Cg");
}

 .widget-dropdown > select:focus {
    border-color: #64B5F6;
}

 .widget-dropdown > select:disabled {
    opacity: 0.6;
}

 /* To disable the dotted border in Firefox around select controls.
   See http://stackoverflow.com/a/18853002 */

 .widget-dropdown > select:-moz-focusring {
    color: transparent;
    text-shadow: 0 0 0 #000;
}

 /* Select and SelectMultiple */

 .widget-select {
    width: 300px;
    line-height: 28px;

    /* Because Firefox defines the baseline of a select as the bottom of the
    control, we align the entire control to the top and add padding to the
    select to get an approximate first line baseline alignment. */
    -webkit-box-align: start;
        -ms-flex-align: start;
            align-items: flex-start;
}

 .widget-select > select {
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    outline: none !important;
    overflow: auto;
    height: inherit;

    /* Because Firefox defines the baseline of a select as the bottom of the
    control, we align the entire control to the top and add padding to the
    select to get an approximate first line baseline alignment. */
    padding-top: 5px;
}

 .widget-select > select:focus {
    border-color: #64B5F6;
}

 .wiget-select > select > option {
    padding-left: 4px;
    line-height: 28px;
    /* line-height doesn't work on some browsers for select options */
    padding-top: calc(28px - var(--jp-widgets-font-size) / 2);
    padding-bottom: calc(28px - var(--jp-widgets-font-size) / 2);
}

 /* Toggle Buttons Styling */

 .widget-toggle-buttons {
    line-height: 28px;
}

 .widget-toggle-buttons .widget-toggle-button {
    margin-left: 2px;
    margin-right: 2px;
}

 .widget-toggle-buttons .jupyter-button:disabled {
    opacity: 0.6;
}

 /* Radio Buttons Styling */

 .widget-radio {
    width: 300px;
    line-height: 28px;
}

 .widget-radio-box {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-bottom: 8px;
}

 .widget-radio-box label {
    height: 20px;
    line-height: 20px;
    font-size: 13px;
}

 .widget-radio-box input {
    height: 20px;
    line-height: 20px;
    margin: 0 8px 0 1px;
    float: left;
}

 /* Color Picker Styling */

 .widget-colorpicker {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-colorpicker > .widget-colorpicker-input {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    min-width: 72px;
}

 .widget-colorpicker input[type="color"] {
    width: 28px;
    height: 28px;
    padding: 0 2px; /* make the color square actually square on Chrome on OS X */
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    border-left: none;
    -webkit-box-flex: 0;
        -ms-flex-positive: 0;
            flex-grow: 0;
    -ms-flex-negative: 0;
        flex-shrink: 0;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    -ms-flex-item-align: stretch;
        align-self: stretch;
    outline: none !important;
}

 .widget-colorpicker.concise input[type="color"] {
    border-left: 1px solid #9E9E9E;
}

 .widget-colorpicker input[type="color"]:focus, .widget-colorpicker input[type="text"]:focus {
    border-color: #64B5F6;
}

 .widget-colorpicker input[type="text"] {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    outline: none !important;
    height: 28px;
    line-height: 28px;
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    font-size: 13px;
    padding: 4px 8px;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -ms-flex-negative: 1;
        flex-shrink: 1;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
}

 .widget-colorpicker input[type="text"]:disabled {
    opacity: 0.6;
}

 /* Date Picker Styling */

 .widget-datepicker {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-datepicker input[type="date"] {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    outline: none !important;
    height: 28px;
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    padding: 4px 8px;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
}

 .widget-datepicker input[type="date"]:focus {
    border-color: #64B5F6;
}

 .widget-datepicker input[type="date"]:invalid {
    border-color: #FF9800;
}

 .widget-datepicker input[type="date"]:disabled {
    opacity: 0.6;
}

 /* Play Widget */

 .widget-play {
    width: 148px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .widget-play .jupyter-button {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    height: auto;
}

 .widget-play .jupyter-button:disabled {
    opacity: 0.6;
}

 /* Tab Widget */

 .jupyter-widgets.widget-tab {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar {
    /* Necessary so that a tab can be shifted down to overlay the border of the box below. */
    overflow-x: visible;
    overflow-y: visible;
}

 .jupyter-widgets.widget-tab > .p-TabBar > .p-TabBar-content {
    /* Make sure that the tab grows from bottom up */
    -webkit-box-align: end;
        -ms-flex-align: end;
            align-items: flex-end;
    min-width: 0;
    min-height: 0;
}

 .jupyter-widgets.widget-tab > .widget-tab-contents {
    width: 100%;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    margin: 0;
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    padding: 15px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    overflow: auto;
}

 .jupyter-widgets.widget-tab > .p-TabBar {
    font: 13px Helvetica, Arial, sans-serif;
    min-height: 25px;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab {
    -webkit-box-flex: 0;
        -ms-flex: 0 1 144px;
            flex: 0 1 144px;
    min-width: 35px;
    min-height: 25px;
    line-height: 24px;
    margin-left: -1px;
    padding: 0px 10px;
    background: #EEEEEE;
    color: rgba(0, 0, 0, .5);
    border: 1px solid #9E9E9E;
    border-bottom: none;
    position: relative;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-current {
    color: rgba(0, 0, 0, 1.0);
    /* We want the background to match the tab content background */
    background: white;
    min-height: 26px;
    -webkit-transform: translateY(1px);
            transform: translateY(1px);
    overflow: visible;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-current:before {
    position: absolute;
    top: -1px;
    left: -1px;
    content: '';
    height: 2px;
    width: calc(100% + 2px);
    background: #2196F3;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab:first-child {
    margin-left: 0;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab:hover:not(.p-mod-current) {
    background: white;
    color: rgba(0, 0, 0, .8);
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-mod-closable > .p-TabBar-tabCloseIcon {
    margin-left: 4px;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-mod-closable > .p-TabBar-tabCloseIcon:before {
    font-family: FontAwesome;
    content: '\F00D'; /* close */
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabIcon,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabLabel,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabCloseIcon {
    line-height: 24px;
}

 /* Accordion Widget */

 .p-Collapse {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .p-Collapse-header {
    padding: 4px;
    cursor: pointer;
    color: rgba(0, 0, 0, .5);
    background-color: #EEEEEE;
    border: 1px solid #9E9E9E;
    padding: 10px 15px;
    font-weight: bold;
}

 .p-Collapse-header:hover {
    background-color: white;
    color: rgba(0, 0, 0, .8);
}

 .p-Collapse-open > .p-Collapse-header {
    background-color: white;
    color: rgba(0, 0, 0, 1.0);
    cursor: default;
    border-bottom: none;
}

 .p-Collapse .p-Collapse-header::before {
    content: '\F0DA\A0';  /* caret-right, non-breaking space */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

 .p-Collapse-open > .p-Collapse-header::before {
    content: '\F0D7\A0'; /* caret-down, non-breaking space */
}

 .p-Collapse-contents {
    padding: 15px;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    border-left: 1px solid #9E9E9E;
    border-right: 1px solid #9E9E9E;
    border-bottom: 1px solid #9E9E9E;
    overflow: auto;
}

 .p-Accordion {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .p-Accordion .p-Collapse {
    margin-bottom: 0;
}

 .p-Accordion .p-Collapse + .p-Collapse {
    margin-top: 4px;
}

 /* HTML widget */

 .widget-html, .widget-htmlmath {
    font-size: 13px;
}

 .widget-html > .widget-html-content, .widget-htmlmath > .widget-html-content {
    /* Fill out the area in the HTML widget */
    -ms-flex-item-align: stretch;
        align-self: stretch;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    /* Makes sure the baseline is still aligned with other elements */
    line-height: 28px;
    /* Make it possible to have absolutely-positioned elements in the html */
    position: relative;
}
</style><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/firstline-fold" src="./README_files/firstline-fold.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/magic-fold" src="./README_files/magic-fold.js.download"></script><link id="favicon" type="image/x-icon" rel="shortcut icon" href="http://localhost:8888/static/base/images/favicon-notebook.ico"><style type="text/css">@font-face {font-family: STIXMathJax_Main-italic; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/STIX-Web/woff/STIXMathJax_Main-Italic.woff?V=2.7.4') format('woff'), url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/STIX-Web/otf/STIXMathJax_Main-Italic.otf?V=2.7.4') format('opentype')}
</style><style type="text/css">@font-face {font-family: STIXMathJax_Main; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/STIX-Web/woff/STIXMathJax_Main-Regular.woff?V=2.7.4') format('woff'), url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/STIX-Web/otf/STIXMathJax_Main-Regular.otf?V=2.7.4') format('opentype')}
</style></head>

<body class="notebook_app command_mode" data-jupyter-api-token="f48477476ef149b8b3aee315c969d0661916ec01139668c8" data-base-url="/" data-ws-url="" data-notebook-name="Untitled1.ipynb" data-notebook-path="Documents/Course-Material/Course_Material/S_16_PCA/Untitled1.ipynb" dir="ltr" style=""><div style="visibility: hidden; overflow: hidden; position: absolute; top: 0px; height: 1px; width: auto; padding: 0px; border: 0px; margin: 0px; text-align: left; text-indent: 0px; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal;"><div id="MathJax_Hidden"><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br></div></div><div id="MathJax_Message" style="display: none;"></div>

<noscript>
    <div id='noscript'>
      Jupyter Notebook requires JavaScript.<br>
      Please enable it to proceed. 
  </div>
</noscript>

<div id="header" style="display: block;">
  <div id="header-container" class="container">
  <div id="ipython_notebook" class="nav navbar-brand"><a href="http://localhost:8888/tree?token=f48477476ef149b8b3aee315c969d0661916ec01139668c8" title="dashboard">
      <img src="./README_files/logo.png" alt="Jupyter Notebook">
  </a></div>

  


<span id="save_widget" class="save_widget">
    <span id="notebook_name" class="filename">Iris_Dataset_Project</span>
    <span class="checkpoint_status" title="ven. 1 mars 2019 10:10">Last Checkpoint: il y a 36 minutes</span>
    <span class="autosave_status">(autosaved)</span>
<i id="notebook-trusted-indicator" class="fa notebook-trusted fa-check" title="Notebook is trusted"></i></span>

<span id="kernel_logo_widget">
  
  <img class="current_kernel_logo" alt="Current Kernel Logo" src="./README_files/logo-64x64.png" title="Python 3" style="display: inline;">
  
</span>


  
  
  
  

    <span id="login_widget">
      
        <button id="logout" class="btn btn-sm navbar-btn">Logout</button>
      
    </span>

  

  
  
  </div>
  <div class="header-bar"></div>

  
<div id="menubar-container" class="container">
<div id="menubar">
    <div id="menus" class="navbar navbar-default" role="navigation">
        <div class="container-fluid">
            <button type="button" class="btn btn-default navbar-btn navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
              <i class="fa fa-bars"></i>
              <span class="navbar-text">Menu</span>
            </button>
            <p id="kernel_indicator" class="navbar-text indicator_area">
              <span class="kernel_indicator_name">Python 3</span>
              <i id="kernel_indicator_icon" class="kernel_idle_icon" title="Kernel Idle"></i>
            </p>
            <i id="readonly-indicator" class="navbar-text" title="This notebook is read-only" style="display: none;">
                <span class="fa-stack">
                    <i class="fa fa-save fa-stack-1x"></i>
                    <i class="fa fa-ban fa-stack-2x text-danger"></i>
                </span>
            </i>
            <i id="modal_indicator" class="navbar-text modal_indicator" title="Command Mode"></i>
            <span id="notification_area"><div id="notification_kernel" class="notification_widget btn btn-xs navbar-btn undefined info" style="display: none;"><span></span></div><div id="notification_notebook" class="notification_widget btn btn-xs navbar-btn" style="display: none;"><span></span></div><div id="notification_trusted" class="notification_widget btn btn-xs navbar-btn" disabled="disabled" style="cursor: help;"><span title="Javascript enabled for notebook display">Trusted</span></div><div id="notification_widgets" class="notification_widget btn btn-xs navbar-btn" style="display: none;"><span></span></div></span>
            <div class="navbar-collapse collapse">
              <ul class="nav navbar-nav">
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">File</a>
                    <ul id="file_menu" class="dropdown-menu">
                        <li id="new_notebook" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">New Notebook</a>
                            <ul class="dropdown-menu" id="menu-new-notebook-submenu"><li id="new-notebook-submenu-python3"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Python 3</a></li></ul>
                        </li>
                        <li id="open_notebook" title="Opens a new window with the Dashboard view">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Open...</a></li>
                        <!-- <hr/> -->
                        <li class="divider"></li>
                        <li id="copy_notebook" title="Open a copy of this notebook&#39;s contents and start a new kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Make a Copy...</a></li>
                        <li id="save_notebook_as" title="Save a copy of the notebook&#39;s contents and start a new kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Save as...</a></li>
                        <li id="rename_notebook"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Rename...</a></li>
                        <li id="save_checkpoint"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Save and Checkpoint</a></li>
                        <!-- <hr/> -->
                        <li class="divider"></li>
                        <li id="restore_checkpoint" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Revert to Checkpoint</a>
                          <ul class="dropdown-menu"><li><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">vendredi 1 mars 2019 10:10</a></li></ul>
                        </li>
                        <li class="divider"></li>
                        <li id="print_preview"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Print Preview</a></li>
                        <li class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Download as</a>
                            <ul id="download_menu" class="dropdown-menu">
                                <li id="download_ipynb"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Notebook (.ipynb)</a></li>
                                <li id="download_script"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Python (.py)</a></li>
                                <li id="download_html"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">HTML (.html)</a></li>
                                <li id="download_slides"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Reveal.js slides (.html)</a></li>
                                <li id="download_markdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Markdown (.md)</a></li>
                                <li id="download_rst"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">reST (.rst)</a></li>
                                <li id="download_latex"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">LaTeX (.tex)</a></li>
                                <li id="download_pdf"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">PDF via LaTeX (.pdf)</a></li>
                                
                                <li id="download_asciidoc">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">asciidoc (.asciidoc)</a>
                                </li>
                                
                                <li id="download_custom">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">custom (.txt)</a>
                                </li>
                                
                                <li id="download_html">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_ch">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_embed">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_toc">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_with_toclenvs">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_latex">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">latex (.tex)</a>
                                </li>
                                
                                <li id="download_latex_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">latex (.tex)</a>
                                </li>
                                
                                <li id="download_markdown">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">markdown (.md)</a>
                                </li>
                                
                                <li id="download_notebook">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">notebook (.ipynb)</a>
                                </li>
                                
                                <li id="download_pdf">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">pdf (.tex)</a>
                                </li>
                                
                                <li id="download_python">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">python (.py)</a>
                                </li>
                                
                                <li id="download_rst">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">rst (.rst)</a>
                                </li>
                                
                                <li id="download_script">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">custom (.txt)</a>
                                </li>
                                
                                <li id="download_selectLanguage">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">notebook (.ipynb)</a>
                                </li>
                                
                                <li id="download_slides">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">slides (.slides.html)</a>
                                </li>
                                
                                <li id="download_slides_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">slides (.slides.html)</a>
                                </li>
                                
                            <li id="download_html_embed"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">HTML Embedded (.html)</a></li></ul>
                        </li>
                        <li class="dropdown-submenu hidden"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Deploy as</a>
                            <ul id="deploy_menu" class="dropdown-menu"></ul>
                        </li>
                        <li class="divider"></li>
                        <li id="trust_notebook" title="Trust the output of this notebook" class="disabled">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Trusted Notebook</a></li>
                        <li class="divider"></li>
                        <li id="close_and_halt" title="Shutdown this notebook&#39;s kernel, and close this window">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Close and Halt</a></li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Edit</a>
                    <ul id="edit_menu" class="dropdown-menu">
                        <li id="cut_cell"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Cut Cells</a></li>
                        <li id="copy_cell"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Copy Cells</a></li>
                        <li id="paste_cell_above" class=""><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Paste Cells Above</a></li>
                        <li id="paste_cell_below" class=""><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Paste Cells Below</a></li>
                        <li id="paste_cell_replace" class=""><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Paste Cells &amp; Replace</a></li>
                        <li id="delete_cell"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Delete Cells</a></li>
                        <li id="undelete_cell" class=""><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Undo Delete Cells</a></li>
                        <li class="divider"></li>
                        <li id="split_cell"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Split Cell</a></li>
                        <li id="merge_cell_above"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Merge Cell Above</a></li>
                        <li id="merge_cell_below"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Merge Cell Below</a></li>
                        <li class="divider"></li>
                        <li id="move_cell_up"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Move Cell Up</a></li>
                        <li id="move_cell_down"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Move Cell Down</a></li>
                        <li class="divider"></li>
                        <li id="edit_nb_metadata"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Edit Notebook Metadata</a></li>
                        <li class="divider"></li>
                        <li id="find_and_replace"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#"> Find and Replace </a></li>
                        <li class="divider"></li>
                        <li id="cut_cell_attachments"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Cut Cell Attachments</a></li>
                        <li id="copy_cell_attachments"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Copy Cell Attachments</a></li>
                        <li id="paste_cell_attachments" class="disabled"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Paste Cell Attachments</a></li>
                        <li class="divider"></li>
                        <li id="insert_image" class="disabled"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#"> Insert Image </a></li>
                    <li class="divider"></li><li><a target="_blank" title="Opens in a new window" href="http://localhost:8888/nbextensions/"> <i class="fa fa-cogs menu-icon pull-right"></i><span>nbextensions config</span></a></li></ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">View</a>
                    <ul id="view_menu" class="dropdown-menu">
                        <li id="toggle_header" title="Show/Hide the logo and notebook title (above menu bar)">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Toggle Header</a>
                        </li>
                        <li id="toggle_toolbar" title="Show/Hide the action icons (below menu bar)">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Toggle Toolbar</a>
                        </li>
                        <li id="toggle_line_numbers" title="Show/Hide line numbers in cells">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Toggle Line Numbers</a>
                        </li>
                        <li id="menu-cell-toolbar" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Cell Toolbar</a>
                            <ul class="dropdown-menu" id="menu-cell-toolbar-submenu"><li data-name="None"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">None</a></li><li data-name="Edit%20Metadata"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Edit Metadata</a></li><li data-name="Raw%20Cell%20Format"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Raw Cell Format</a></li><li data-name="Slideshow"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Slideshow</a></li><li data-name="Attachments"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Attachments</a></li><li data-name="Tags"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Tags</a></li></ul>
                        </li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Insert</a>
                    <ul id="insert_menu" class="dropdown-menu">
                        <li id="insert_cell_above" title="Insert an empty Code cell above the currently active cell">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Insert Cell Above</a></li>
                        <li id="insert_cell_below" title="Insert an empty Code cell below the currently active cell">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Insert Cell Below</a></li>
                    <li class="divider"></li><li><a title="Insert a heading cell above the selected cell" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Insert Heading Above</a></li><li><a title="Insert a heading cell below the selected cell&#39;s section" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Insert Heading Below</a></li></ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Cell</a>
                    <ul id="cell_menu" class="dropdown-menu">
                        <li id="run_cell" title="Run this cell, and move cursor to the next one">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Run Cells</a></li>
                        <li id="run_cell_select_below" title="Run this cell, select below">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Run Cells and Select Below</a></li>
                        <li id="run_cell_insert_below" title="Run this cell, insert below">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Run Cells and Insert Below</a></li>
                        <li id="run_all_cells" title="Run all cells in the notebook">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Run All</a></li>
                        <li id="run_all_cells_above" title="Run all cells above (but not including) this cell">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Run All Above</a></li>
                        <li id="run_all_cells_below" title="Run this cell and all cells below it">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Run All Below</a></li>
                        <li class="divider"></li>
                        <li id="change_cell_type" class="dropdown-submenu" title="All cells in the notebook have a cell type. By default, new cells are created as &#39;Code&#39; cells">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Cell Type</a>
                            <ul class="dropdown-menu">
                              <li id="to_code" title="Contents will be sent to the kernel for execution, and output will display in the footer of cell">
                                  <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Code</a></li>
                              <li id="to_markdown" title="Contents will be rendered as HTML and serve as explanatory text">
                                  <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Markdown</a></li>
                              <li id="to_raw" title="Contents will pass through nbconvert unmodified">
                                  <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Raw NBConvert</a></li>
                            </ul>
                        </li>
                        <li class="divider"></li>
                        <li id="current_outputs" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Current Outputs</a>
                            <ul class="dropdown-menu">
                                <li id="toggle_current_output" title="Hide/Show the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Toggle</a>
                                </li>
                                <li id="toggle_current_output_scroll" title="Scroll the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Toggle Scrolling</a>
                                </li>
                                <li id="clear_current_output" title="Clear the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Clear</a>
                                </li>
                            </ul>
                        </li>
                        <li id="all_outputs" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">All Output</a>
                            <ul class="dropdown-menu">
                                <li id="toggle_all_output" title="Hide/Show the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Toggle</a>
                                </li>
                                <li id="toggle_all_output_scroll" title="Scroll the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Toggle Scrolling</a>
                                </li>
                                <li id="clear_all_output" title="Clear the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Clear</a>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Kernel</a>
                    <ul id="kernel_menu" class="dropdown-menu">
                        <li id="int_kernel" title="Send Keyboard Interrupt (CTRL-C) to the Kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Interrupt</a>
                        </li>
                        <li id="restart_kernel" title="Restart the Kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Restart</a>
                        </li>
                        <li id="restart_clear_output" title="Restart the Kernel and clear all output">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Restart &amp; Clear Output</a>
                        </li>
                        <li id="restart_run_all" title="Restart the Kernel and re-run the notebook">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Restart &amp; Run All</a>
                        </li>
                        <li id="reconnect_kernel" title="Reconnect to the Kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Reconnect</a>
                        </li>
                        <li id="shutdown_kernel" title="Shutdown the Kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Shutdown</a>
                        </li>
                        <li class="divider"></li>
                        <li id="menu-change-kernel" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Change kernel</a>
                            <ul class="dropdown-menu" id="menu-change-kernel-submenu"><li id="kernel-submenu-python3"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Python 3</a></li></ul>
                        </li>
                    </ul>
                </li><li id="Navigate" class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" id="Navigate_sub" class="dropdown-toggle" data-toggle="dropdown">Navigate</a><ul id="Navigate_menu" class="dropdown-menu ui-resizable" style=""><div id="navigate_menu" class="toc" style="width: 160px; height: 0px;"><ul class="toc-item"><li><span><i class="fa fa-fw fa-caret-down"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Principal-Component-Analysis-with-scikit-learn-in-Python----Project-Overview" data-toc-modified-id="Principal-Component-Analysis-with-scikit-learn-in-Python----Project-Overview-1" class="toc-item-highlight-select"><span class="toc-item-num">1&nbsp;&nbsp;</span>Principal Component Analysis with scikit-learn in Python -- Project Overview</a></span><ul class="toc-item"><li><ul class="toc-item"><li><span><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Principal-Component-Analysis-(PCA)" data-toc-modified-id="Principal-Component-Analysis-(PCA)-1.0.1"><span class="toc-item-num">1.0.1&nbsp;&nbsp;</span>Principal Component Analysis (PCA)</a></span></li></ul></li><li><span><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#SVM-on-Principal-Components" data-toc-modified-id="SVM-on-Principal-Components-1.1" class=""><span class="toc-item-num">1.1&nbsp;&nbsp;</span>SVM on Principal Components</a></span></li></ul></li></ul></div><div class="ui-resizable-handle ui-resizable-e" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div></ul></li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" data-toggle="dropdown" class="dropdown-toggle">Widgets</a><ul id="widget-submenu" class="dropdown-menu"><li title="Save the notebook with the widget state information for static rendering"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Save Notebook Widget State</a></li><li title="Clear the widget state information from the notebook"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Clear Notebook Widget State</a></li><ul class="divider"></ul><li title="Download the widget state as a JSON file"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Download Widget State</a></li><li title="Embed interactive widgets"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Embed Widgets</a></li></ul></li><li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Help</a>
                    <ul id="help_menu" class="dropdown-menu">
                        
                        <li id="notebook_tour" title="A quick tour of the notebook user interface"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">User Interface Tour</a></li>
                        <li id="keyboard_shortcuts" title="Opens a tooltip with all keyboard shortcuts"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Keyboard Shortcuts</a></li>
                        <li id="edit_keyboard_shortcuts" title="Opens a dialog allowing you to edit Keyboard shortcuts"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">Edit Keyboard Shortcuts</a></li>
                        <li class="divider"></li>
                        

						
                        
                            
                                <li><a rel="noreferrer" href="http://nbviewer.jupyter.org/github/ipython/ipython/blob/3.x/examples/Notebook/Index.ipynb" target="_blank" title="Opens in a new window">
                                
                                    <i class="fa fa-external-link menu-icon pull-right"></i>
                                

                                Notebook Help
                                </a></li>
                            
                                <li><a rel="noreferrer" href="https://help.github.com/articles/markdown-basics/" target="_blank" title="Opens in a new window">
                                
                                    <i class="fa fa-external-link menu-icon pull-right"></i>
                                

                                Markdown
                                </a></li>
                            
                            
                        
                        <li><a title="Jupyter_contrib_nbextensions documentation" id="jupyter_contrib_nbextensions_help" href="http://jupyter-contrib-nbextensions.readthedocs.io/en/latest/" target="_blank">Jupyter-contrib <br> nbextensions<i class="fa fa-external-link menu-icon pull-right"></i></a></li><li id="kernel-help-links" class="divider"></li><li><a target="_blank" title="Opens in a new window" href="https://docs.python.org/3.7?v=20190301082907"><i class="fa fa-external-link menu-icon pull-right"></i><span>Python Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://ipython.org/documentation.html?v=20190301082907"><i class="fa fa-external-link menu-icon pull-right"></i><span>IPython Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://docs.scipy.org/doc/numpy/reference/?v=20190301082907"><i class="fa fa-external-link menu-icon pull-right"></i><span>NumPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://docs.scipy.org/doc/scipy/reference/?v=20190301082907"><i class="fa fa-external-link menu-icon pull-right"></i><span>SciPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://matplotlib.org/contents.html?v=20190301082907"><i class="fa fa-external-link menu-icon pull-right"></i><span>Matplotlib Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="http://docs.sympy.org/latest/index.html?v=20190301082907"><i class="fa fa-external-link menu-icon pull-right"></i><span>SymPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://pandas.pydata.org/pandas-docs/stable/?v=20190301082907"><i class="fa fa-external-link menu-icon pull-right"></i><span>pandas Reference</span></a></li><li class="divider"></li>
                        <li title="About Jupyter Notebook"><a id="notebook_about" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#">About</a></li>
                        
                    </ul>
                </li>
              </ul>
            </div>
        </div>
    </div>
</div>

<div id="maintoolbar" class="navbar">
  <div class="toolbar-inner navbar-inner navbar-nobg">
    <div id="maintoolbar-container" class="container toolbar"><div class="btn-group" id="save-notbook"><button class="btn btn-default" title="Save and Checkpoint" data-jupyter-action="jupyter-notebook:save-notebook"><i class="fa-save fa"></i></button></div><div class="btn-group" id="insert_above_below"><button class="btn btn-default" title="insert cell below" data-jupyter-action="jupyter-notebook:insert-cell-below"><i class="fa-plus fa"></i></button></div><div class="btn-group" id="cut_copy_paste"><button class="btn btn-default" title="cut selected cells" data-jupyter-action="jupyter-notebook:cut-cell"><i class="fa-cut fa"></i></button><button class="btn btn-default" title="copy selected cells" data-jupyter-action="jupyter-notebook:copy-cell"><i class="fa-copy fa"></i></button><button class="btn btn-default" title="paste cells below" data-jupyter-action="jupyter-notebook:paste-cell-below"><i class="fa-paste fa"></i></button></div><div class="btn-group" id="move_up_down"><button class="btn btn-default" title="move selected cells up" data-jupyter-action="jupyter-notebook:move-cell-up"><i class="fa-arrow-up fa"></i></button><button class="btn btn-default" title="move selected cells down" data-jupyter-action="jupyter-notebook:move-cell-down"><i class="fa-arrow-down fa"></i></button></div><div class="btn-group" id="run_int"><button class="btn btn-default" title="Run" data-jupyter-action="jupyter-notebook:run-cell-and-select-next"><i class="fa-step-forward fa"></i><span class="toolbar-btn-label">Run</span></button><button class="btn btn-default" title="interrupt the kernel" data-jupyter-action="jupyter-notebook:interrupt-kernel"><i class="fa-stop fa"></i></button><button class="btn btn-default" title="restart the kernel (with dialog)" data-jupyter-action="jupyter-notebook:confirm-restart-kernel"><i class="fa-repeat fa"></i></button><button class="btn btn-default" title="restart the kernel, then re-run the whole notebook (with dialog)" data-jupyter-action="jupyter-notebook:confirm-restart-kernel-and-run-all-cells"><i class="fa-forward fa"></i></button></div><select id="cell_type" class="form-control select-xs"><option value="code">Code</option><option value="markdown">Markdown</option><option value="raw">Raw NBConvert</option><option value="heading">Heading</option><option value="multiselect" disabled="disabled" style="display: none;">-</option></select><div class="btn-group"><button class="btn btn-default" title="open the command palette" data-jupyter-action="jupyter-notebook:show-command-palette"><i class="fa-keyboard-o fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Variable Inspector" data-jupyter-action="varInspector:toggle-variable-inspector" id="varInspector_button"><i class="fa-crosshairs fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Increase code font size" data-jupyter-action="code_font_size:increase-code-font-size"><i class="fa-search-plus fa"></i></button><button class="btn btn-default" title="Decrease code font size" data-jupyter-action="code_font_size:decrease-code-font-size"><i class="fa-search-minus fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Create/Edit Gist of Notebook" data-jupyter-action="gist_it:create-gist-from-notebook"><i class="fa-github fa"></i></button></div><div class="btn-group" id="code_prettify_button"><button class="btn btn-default" title="code_prettify selected cell(s) (add shift for all cells)"><i class="fa-legal fa"></i></button></div><div class="btn-group" id="autopep8_button"><button class="btn btn-default" title="autopep8 selected cell(s) (add shift for all cells)"><i class="fa-legal fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Table of Contents" data-jupyter-action="toc2:toggle-toc" id="toc_button"><i class="fa-list fa"></i></button></div></div>
  </div>
</div>
</div>

<div class="lower-header-bar"></div>

</div>

<div id="site" style="display: block; height: 607.444px;"><div id="toc-wrapper" class="ui-draggable ui-resizable sidebar-wrapper" style="display: none; position: relative; width: 20%; top: 163.333px; left: 0px;"><div id="toc-header"><span class="header">Contents </span><i class="fa fa-fw hide-btn" title="Hide ToC"></i><i class="fa fa-fw fa-refresh" title="Reload ToC"></i><i class="fa fa-fw fa-cog" title="ToC settings"></i></div><div id="toc" class="toc"><ul class="toc-item"><li><span class="highlight_on_scroll"><i class="fa fa-fw fa-caret-down"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Principal-Component-Analysis-with-scikit-learn-in-Python----Project-Overview" data-toc-modified-id="Principal-Component-Analysis-with-scikit-learn-in-Python----Project-Overview-1" class="toc-item-highlight-select"><span class="toc-item-num">1&nbsp;&nbsp;</span>Principal Component Analysis with scikit-learn in Python -- Project Overview</a></span><ul class="toc-item"><li><ul class="toc-item"><li><span class=""><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Principal-Component-Analysis-(PCA)" data-toc-modified-id="Principal-Component-Analysis-(PCA)-1.0.1"><span class="toc-item-num">1.0.1&nbsp;&nbsp;</span>Principal Component Analysis (PCA)</a></span></li></ul></li><li><span class=""><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#SVM-on-Principal-Components" data-toc-modified-id="SVM-on-Principal-Components-1.1" class=""><span class="toc-item-num">1.1&nbsp;&nbsp;</span>SVM on Principal Components</a></span></li></ul></li></ul></div><div class="ui-resizable-handle ui-resizable-n" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-e ui-icon ui-icon-grip-dotted-vertical" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-w" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-sw" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-ne" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-nw" style="z-index: 90;"></div></div>


<div id="ipython-main-app">
    <div id="notebook_panel">
        <div id="notebook" tabindex="-1"><div class="container" id="notebook-container"><div class="cell text_cell collapsible_headings_ellipsis rendered selected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h1"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 28.7083px; left: 366.667px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 54px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 366.667px; top: 23.1111px; height: 19.5556px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-1"># Principal Component Analysis with scikit-learn in Python -- Project Overview</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 54px;"></div><div class="CodeMirror-gutters" style="height: 65px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h1 id="Principal-Component-Analysis-with-scikit-learn-in-Python----Project-Overview" data-toc-modified-id="Principal-Component-Analysis-with-scikit-learn-in-Python----Project-Overview-1"><a class="toc-mod-link" id="Principal-Component-Analysis-with-scikit-learn-in-Python----Project-Overview-1"></a><span class="toc-item-num">1&nbsp;&nbsp;</span>Principal Component Analysis with scikit-learn in Python -- Project Overview<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Principal-Component-Analysis-with-scikit-learn-in-Python----Project-Overview">¶</a></h1>
</div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 38.9306px; left: 174.931px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 62px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 174.931px; top: 33.3333px; height: 17.3333px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">We going to use for this project the famous IRIS data set. The IRIS data have only 4 features and may not be ideal dataset for PCA. However, our goal is just to illustrate the PCA.</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 62px;"></div><div class="CodeMirror-gutters" style="height: 73px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><p>We going to use for this project the famous IRIS data set. The IRIS data have only 4 features and may not be ideal dataset for PCA. However, our goal is just to illustrate the PCA.</p>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 403.375px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 403.375px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's import the libraries needed and load the dataset</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-import-the-libraries-needed-and-load-the-dataset">Let's import the libraries needed and load the dataset<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-import-the-libraries-needed-and-load-the-dataset">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[1]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 18.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 247.181px; margin-bottom: -19px; border-right-width: 11px; min-height: 96px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>5</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">matplotlib</span>.<span class="cm-property">pyplot</span> <span class="cm-keyword">as</span> <span class="cm-variable">plt</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">pandas</span> <span class="cm-keyword">as</span> <span class="cm-variable">pd</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">numpy</span> <span class="cm-keyword">as</span> <span class="cm-variable">np</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">seaborn</span> <span class="cm-keyword">as</span> <span class="cm-variable">sns</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-operator">%</span><span class="cm-variable">matplotlib</span> <span class="cm-variable">inline</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 96px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 107px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 222.111px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 222.111px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's load the IRIS dataset</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-load-the-IRIS-dataset">Let's load the IRIS dataset<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-load-the-IRIS-dataset">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[2]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.4863px; left: 149.417px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 300.778px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>2</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 136.417px; top: 16.8889px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">datasets</span> <span class="cm-keyword">import</span> <span class="cm-variable">load_iris</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">iris</span> <span class="cm-operator">=</span> <span class="cm-variable">load_iris</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 56px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 527.111px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 527.111px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's acces iris which is a dictionary-like object by using .keys() method</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-acces-iris-which-is-a-dictionary-like-object-by-using-.keys()-method">Let's acces iris which is a dictionary-like object by using .keys() method<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-acces-iris-which-is-a-dictionary-like-object-by-using-.keys()-method">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[3]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 95.5417px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 93.2361px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 82.5417px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">iris</span>.<span class="cm-property">keys</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[3]:</bdi></div><div class="output_subarea output_text output_result"><pre>dict_keys(['data', 'target', 'target_names', 'DESCR', 'feature_names', 'filename'])</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 23.375px; left: 192.889px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 47px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 192.889px; top: 17.7777px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's create the dataframe and output the head of the data, and let's use features_names as columns</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 47px;"></div><div class="CodeMirror-gutters" style="height: 58px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-create-the-dataframe-and-output-the-head-of-the-data,-and-let&#39;s-use-features_names-as-columns">Let's create the dataframe and output the head of the data, and let's use features_names as columns<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-create-the-dataframe-and-output-the-head-of-the-data,-and-let&#39;s-use-features_names-as-columns">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[5]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 39.3752px; left: 249.486px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 239.486px; margin-bottom: -19px; border-right-width: 11px; min-height: 62px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>3</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 236.486px; top: 33.7778px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span> <span class="cm-operator">=</span> <span class="cm-variable">pd</span>.<span class="cm-property">DataFrame</span><span class=" CodeMirror-matchingbracket">(</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">iris</span>[<span class="cm-string">'data'</span>],</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">columns</span><span class="cm-operator">=</span><span class="cm-variable">iris</span>[<span class="cm-string">'feature_names'</span>]<span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 62px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 73px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[6]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 80.1528px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 77.8472px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 67.1528px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>.<span class="cm-property">head</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[6]:</bdi></div><div class="output_subarea output_html rendered_html output_result"><div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 371.514px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 371.514px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's import StandScaler and create its instance </span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-import-StandScaler-and-create-its-instance">Let's import StandScaler and create its instance<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-import-StandScaler-and-create-its-instance">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[7]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 39.3749px; left: 80.1667px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 378.014px; margin-bottom: -19px; border-right-width: 11px; min-height: 62px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>3</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 67.1667px; top: 33.7778px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">preprocessing</span> <span class="cm-keyword">import</span> <span class="cm-variable">StandardScaler</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-comment"># the instance</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">scaler</span> <span class="cm-operator">=</span> <span class="cm-variable">StandardScaler</span>()</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 62px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 73px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 346.583px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 346.583px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's fit the scaler to the features in our data </span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-fit-the-scaler-to-the-features-in-our-data">Let's fit the scaler to the features in our data<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-fit-the-scaler-to-the-features-in-our-data">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[8]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 126.333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 116.333px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 113.333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">scaler</span>.<span class="cm-property">fit</span><span class=" CodeMirror-matchingbracket">(</span><span class="cm-variable">df</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[8]:</bdi></div><div class="output_subarea output_text output_result"><pre>StandardScaler(copy=True, with_mean=True, with_std=True)</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 349.333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 349.333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's transform the dataset to the scaled data</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-transform-the-dataset-to-the-scaled-data">Let's transform the dataset to the scaled data<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-transform-the-dataset-to-the-scaled-data">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[12]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 87.8611px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 254.861px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 74.8611px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df_scaled</span> <span class="cm-operator">=</span> <span class="cm-variable">scaler</span>.<span class="cm-property">transform</span>(<span class="cm-variable">df</span>)</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h3"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 354.667px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 30px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 354.667px; top: 0px; height: 18.6667px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-3">### Principal Component Analysis (PCA)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 30px;"></div><div class="CodeMirror-gutters" style="height: 41px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h3 id="Principal-Component-Analysis-(PCA)" data-toc-modified-id="Principal-Component-Analysis-(PCA)-1.0.1"><a class="toc-mod-link" id="Principal-Component-Analysis-(PCA)-1.0.1"></a><span class="toc-item-num">1.0.1&nbsp;&nbsp;</span>Principal Component Analysis (PCA)<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Principal-Component-Analysis-(PCA)">¶</a></h3>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 23.375px; left: 259.181px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 47px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 259.181px; top: 17.7778px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's import PCA and create its instance, and let's see what should we do if we are interested in only first 2 components?</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 47px;"></div><div class="CodeMirror-gutters" style="height: 58px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-import-PCA-and-create-its-instance,-and-let&#39;s-see-what-should-we-do-if-we-are-interested-in-only-first-2-components?">Let's import PCA and create its instance, and let's see what should we do if we are interested in only first 2 components?<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-import-PCA-and-create-its-instance,-and-let&#39;s-see-what-should-we-do-if-we-are-interested-in-only-first-2-components?">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[13]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 103.667px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 293.347px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>2</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 90.6667px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">decomposition</span> <span class="cm-keyword">import</span> <span class="cm-variable">PCA</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">pca</span> <span class="cm-operator">=</span> <span class="cm-variable">PCA</span>(<span class="cm-variable">n_components</span><span class="cm-operator">=</span><span class="cm-number">2</span>)</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 56px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 264.889px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 264.889px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's fit the object to scaled data</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-fit-the-object-to-scaled-data">Let's fit the object to scaled data<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-fit-the-object-to-scaled-data">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[14]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 157.111px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 147.111px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 144.111px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">pca</span>.<span class="cm-property">fit</span><span class=" CodeMirror-matchingbracket">(</span><span class="cm-variable">df_scaled</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[14]:</bdi></div><div class="output_subarea output_text output_result"><pre>PCA(copy=True, iterated_power='auto', n_components=2, random_state=None,
  svd_solver='auto', tol=0.0, whiten=False)</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 313.778px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 313.778px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's transform the data to its first 2PCs</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-transform-the-data-to-its-first-2PCs">Let's transform the data to its first 2PCs<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-transform-the-data-to-its-first-2PCs">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[15]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 257.153px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 247.153px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 244.153px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">pc12</span> <span class="cm-operator">=</span> <span class="cm-variable">pca</span>.<span class="cm-property">transform</span><span class=" CodeMirror-matchingbracket">(</span><span class="cm-variable">df_scaled</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 357.819px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 357.819px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### pc12 is a numpy array, let's create a dataframe</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="pc12-is-a-numpy-array,-let&#39;s-create-a-dataframe">pc12 is a numpy array, let's create a dataframe<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#pc12-is-a-numpy-array,-let&#39;s-create-a-dataframe">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[16]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 95.5417px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 85.5417px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 82.5417px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-builtin">type</span><span class=" CodeMirror-matchingbracket">(</span><span class="cm-variable">pc12</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[16]:</bdi></div><div class="output_subarea output_text output_result"><pre>numpy.ndarray</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[18]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 56.2638px; left: 64.7778px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 201px; margin-bottom: -19px; border-right-width: 11px; min-height: 79px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>4</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 51.7778px; top: 50.6667px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df_pca</span> <span class="cm-operator">=</span> <span class="cm-variable">pd</span>.<span class="cm-property">DataFrame</span>(</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">pc12</span>,</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">columns</span> <span class="cm-operator">=</span> [<span class="cm-string">'PC1'</span>, <span class="cm-string">'PC2'</span>])</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df_pca</span>.<span class="cm-property">head</span>()</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 79px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 90px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[18]:</bdi></div><div class="output_subarea output_html rendered_html output_result"><div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PC1</th>
      <th>PC2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-2.264703</td>
      <td>0.480027</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-2.080961</td>
      <td>-0.674134</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-2.364229</td>
      <td>-0.341908</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-2.299384</td>
      <td>-0.597395</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-2.389842</td>
      <td>0.646835</td>
    </tr>
  </tbody>
</table>
</div></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[20]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59729px; left: 64.7778px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 108.639px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 51.7778px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df_pca</span>.<span class="cm-property">info</span>()</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_text output_stream output_stdout"><pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 150 entries, 0 to 149
Data columns (total 2 columns):
PC1    150 non-null float64
PC2    150 non-null float64
dtypes: float64(2)
memory usage: 2.4 KB
</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 543.111px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 47px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 543.111px; top: 0px; height: 17.7777px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's plot PC1 and PC2, we will pass the target values as c to separate two classes of iris.</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 47px;"></div><div class="CodeMirror-gutters" style="height: 58px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-plot-PC1-and-PC2,-we-will-pass-the-target-values-as-c-to-separate-two-classes-of-iris.">Let's plot PC1 and PC2, we will pass the target values as c to separate two classes of iris.<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-plot-PC1-and-PC2,-we-will-pass-the-target-values-as-c-to-separate-two-classes-of-iris.">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[21]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 140.708px; left: 87.8472px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 362.639px; margin-bottom: -19px; border-right-width: 11px; min-height: 164px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>9</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 74.8472px; top: 135.111px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">figure</span>(<span class="cm-variable">figsize</span><span class="cm-operator">=</span>(<span class="cm-number">10</span>,<span class="cm-number">8</span>))</span></pre><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">scatter</span>(</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">x</span><span class="cm-operator">=</span><span class="cm-variable">df_pca</span>[<span class="cm-string">'PC1'</span>],</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">y</span><span class="cm-operator">=</span><span class="cm-variable">df_pca</span>[<span class="cm-string">'PC2'</span>],</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">c</span><span class="cm-operator">=</span><span class="cm-variable">iris</span>[<span class="cm-string">'target'</span>],</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">cmap</span> <span class="cm-operator">=</span> <span class="cm-string">'Set1'</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">xlabel</span>(<span class="cm-string">'First Principal Component - PC1'</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">ylabel</span>(<span class="cm-string">'Second Principal Component - PC2'</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">show</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 164px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 175px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_png"><img src="data:image/png;base64,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HOHHfUVkPwUCcPLPYMaPYM9m6HkwhHP9jkpEpFtQoXARab9wLvQZ7ncUIiLdSlfY2kJEREQkYykZExEREfGRkjERERERHykZExEREfGRkjERERERHykZExEREfGRkjERERERHykZExEREfGRkjERERERHykZExEREfGRkjERERERHykZExEREfGRkjERERERHykZExEREfFRyO8AJH3FKiqoef11cI7s444jkJ/vd0giIiJpR8mY7Jeq555j15XfgmDQa4hGKbzjdvLOON3fwERERNKMhimlw6IlJez8xjdxVVW48nLvUVVF6be+TXTbNr/DExERSStKxqTDqp58KmG7A6qeeDK1wYiIiKQ5JWPSYa6iAiKR5gfq6rxjIiIi0m5KxqTDck48EULNpxtaVhbZJ53oQ0QiIiLpS8mYdFh47BjyZ12M5eXtbbO8PHIvmEnWuHE+RiYiIpJ+tJpS9kuvW/6HnNNPp/LRR8E58i6YSfZxx/kdloiISNpRMib7xczIOf44co5XAiYiInIgNEwpIiIi4iMlYyIiIiI+UjImIiIi4iMlYyIiIiI+UjImIiIi4iMlYyIiIiI+UjImIiIi4iMlYyIiIiI+UjImIiIi4iMlYyIiIiI+UjImIiIi4iMlYyIiIiI+UjImIiIi4iMlYyIiIiI+UjImIiIi4iMlYyLin+Wz4bfD4adhuGM0rH7c74hERFJOyZiI+OPtv8ITX4PSdRCLwI7V8PAl8N4TfkcmIpJSSsZEJPWcgxdugLrKxu2RKpj3fX9iEhHxiZIxEUm9aB2Ub0l8bNfa1MYiIuIzJWMiknrBMOT1S3ys8BOpjUVExGdKxkQk9czghJsgnNe4PZQHJ93iS0giIn5RMiYi/pjyDTj119BjgPe8YAicczeMvdDfuEREUizkdwAikqHMYMoV3iMWhUDQ74hERHyhnjER8Z8SMRHJYErGRERERHykZExERETER0rGRERERHykZExERETER0rGRERERHykZExERETER0rGRERERHykZExERETER0rGRERERHykZExERETER0rGRERERHykZExERETER0rGRERERHykZExERETER0rGRERERHxkzjm/Y2g3MysB1rdwuB+wPYXhdGf6LDuPPsvOpc+z8+iz7Dz6LDtPd/ssP+GcK2rrpLRKxlpjZoucc5P9jqM70GfZefRZ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"></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 600px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 600px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's see how to get the components by creating a dataframe and outpout its head.</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-see-how-to-get-the-components-by-creating-a-dataframe-and-outpout-its-head.">Let's see how to get the components by creating a dataframe and outpout its head.<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-see-how-to-get-the-components-by-creating-a-dataframe-and-outpout-its-head.">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[22]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 133.889px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 123.889px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 120.889px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">pca</span>.<span class="cm-property">components_</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[22]:</bdi></div><div class="output_subarea output_text output_result"><pre>array([[ 0.52106591, -0.26934744,  0.5804131 ,  0.56485654],
       [ 0.37741762,  0.92329566,  0.02449161,  0.06694199]])</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.0416px; left: 351.972px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 351.972px; top: 16.4445px; height: 17.3333px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">Each row, in this numpy matrix array, represents a principal component, and each column relates back to the original features.</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="height: 56px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><p>Each row, in this numpy matrix array, represents a principal component, and each column relates back to the original features.</p>
</div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.0417px; left: 618px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 621.333px; top: 16.4444px; height: 17.3334px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">Let's convert this numpy array into pandas dataframe and visualize this relationship with a heatmap, we will pass the columns from our original dataset.</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="height: 56px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><p>Let's convert this numpy array into pandas dataframe and visualize this relationship with a heatmap, we will pass the columns from our original dataset.</p>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[23]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 56.2639px; left: 149.431px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 285.653px; margin-bottom: -19px; border-right-width: 11px; min-height: 79px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>4</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 136.431px; top: 50.6667px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df_pca_comp</span> <span class="cm-operator">=</span> <span class="cm-variable">pd</span>.<span class="cm-property">DataFrame</span>(</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">pca</span>.<span class="cm-property">components_</span>,</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">columns</span> <span class="cm-operator">=</span> <span class="cm-variable">iris</span>[<span class="cm-string">'feature_names'</span>])</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df_pca_comp</span>.<span class="cm-property">head</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 79px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 90px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[23]:</bdi></div><div class="output_subarea output_html rendered_html output_result"><div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.521066</td>
      <td>-0.269347</td>
      <td>0.580413</td>
      <td>0.564857</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.377418</td>
      <td>0.923296</td>
      <td>0.024492</td>
      <td>0.066942</td>
    </tr>
  </tbody>
</table>
</div></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[24]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 73.1528px; left: 87.8472px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 208.333px; margin-bottom: -19px; border-right-width: 11px; min-height: 96px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>5</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 74.8472px; top: 67.5556px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">figure</span>(<span class="cm-variable">figsize</span><span class="cm-operator">=</span>(<span class="cm-number">12</span>,<span class="cm-number">6</span>))</span></pre><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">sns</span>.<span class="cm-property">heatmap</span>(</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">df_pca_comp</span>,</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">cmap</span> <span class="cm-operator">=</span> <span class="cm-string">'rainbow'</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">show</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 96px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 107px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_png"><img src="data:image/png;base64,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"></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h2"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 356.278px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 32px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 356.278px; top: 0px; height: 20.4444px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-2">## SVM on Principal Components</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 32px;"></div><div class="CodeMirror-gutters" style="height: 43px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h2 id="SVM-on-Principal-Components" data-toc-modified-id="SVM-on-Principal-Components-1.1"><a class="toc-mod-link" id="SVM-on-Principal-Components-1.1"></a><span class="toc-item-num">1.1&nbsp;&nbsp;</span>SVM on Principal Components<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#SVM-on-Principal-Components">¶</a></h2>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 532px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 532px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's separate features and target classes, and let's do the train test split</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-separate-features-and-target-classes,-and-let&#39;s-do-the-train-test-split">Let's separate features and target classes, and let's do the train test split<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-separate-features-and-target-classes,-and-let&#39;s-do-the-train-test-split">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[25]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 123.819px; left: 341.806px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 408.819px; margin-bottom: -19px; border-right-width: 11px; min-height: 147px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre>x</pre><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>8</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 328.806px; top: 118.222px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-comment">#Separating fearures and target values</span></span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">X</span> <span class="cm-operator">=</span> <span class="cm-variable">df_pca</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">y</span> <span class="cm-operator">=</span> <span class="cm-variable">iris</span>[<span class="cm-string">'target'</span>]</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-comment">#train-test-split</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">model_selection</span> <span class="cm-keyword">import</span> <span class="cm-variable">train_test_split</span></span></pre><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">X_train</span>, <span class="cm-variable">X_test</span>, <span class="cm-variable">y_train</span>, <span class="cm-variable">y_test</span> <span class="cm-operator">=</span> <span class="cm-variable">train_test_split</span><span class=" CodeMirror-matchingbracket">(</span></span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">X</span>, <span class="cm-variable">y</span>, <span class="cm-variable">test_size</span><span class="cm-operator">=</span><span class="cm-number">0.30</span>, <span class="cm-variable">random_state</span><span class="cm-operator">=</span><span class="cm-number">42</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 147px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 158px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 319.375px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 319.375px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's import SVC and create its instance </span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="height: 40px; left: 0px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-import-SVC-and-create-its-instance">Let's import SVC and create its instance<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-import-SVC-and-create-its-instance">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[34]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.4861px; left: 218.694px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1" draggable="false"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 216.333px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre>x</pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 205.694px; top: 16.8889px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">svm</span> <span class="cm-keyword">import</span> <span class="cm-variable">SVC</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">model</span> <span class="cm-operator">=</span> <span class="cm-variable">SVC</span><span class=" CodeMirror-matchingbracket">(</span><span class="cm-variable">gamma</span><span class="cm-operator">=</span><span class="cm-string">'scale'</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 56px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 220.306px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 186.306px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's train our model</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-train-our-model">Let's train our model<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-train-our-model">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[35]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.4861px; left: 18.5972px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 216.389px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>2</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.59723px; top: 16.8889px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">model</span>.<span class="cm-property">fit</span>(<span class="cm-variable">X_train</span>, <span class="cm-variable">y_train</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 56px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[35]:</bdi></div><div class="output_subarea output_text output_result"><pre>SVC(C=1.0, cache_size=200, class_weight=None, coef0=0.0,
  decision_function_shape='ovr', degree=3, gamma='scale', kernel='rbf',
  max_iter=-1, probability=False, random_state=None, shrinking=True,
  tol=0.001, verbose=False)</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 214.444px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 180.444px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's do predictions</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px; display: none;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-do-predictions">Let's do predictions<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-do-predictions">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[37]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 280.278px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 277.972px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre>x</pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 267.278px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">predictions</span> <span class="cm-operator">=</span> <span class="cm-variable">model</span>.<span class="cm-property">predict</span><span class=" CodeMirror-matchingbracket">(</span><span class="cm-variable">X_test</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 586.667px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 586.667px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's an evaluation then print the Classification Report and The Confusion Matrix</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-an-evaluation-then-print-the-Classification-Report-and-The-Confusion-Matrix">Let's an evaluation then print the Classification Report and The Confusion Matrix<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#Let&#39;s-an-evaluation-then-print-the-Classification-Report-and-The-Confusion-Matrix">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[38]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 39.375px; left: 341.861px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 523.889px; margin-bottom: -19px; border-right-width: 11px; min-height: 62px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 328.861px; top: 33.7778px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">metrics</span> <span class="cm-keyword">import</span> <span class="cm-variable">classification_report</span>, <span class="cm-variable">confusion_matrix</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-builtin">print</span>(<span class="cm-variable">classification_report</span>(<span class="cm-variable">y_test</span>, <span class="cm-variable">predictions</span>))</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-builtin">print</span>(<span class="cm-variable">confusion_matrix</span><span class=" CodeMirror-matchingbracket">(</span><span class="cm-variable">y_test</span>, <span class="cm-variable">predictions</span><span class=" CodeMirror-matchingbracket">)</span>)</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 62px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 73px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_text output_stream output_stdout"><pre>              precision    recall  f1-score   support

           0       1.00      1.00      1.00        19
           1       0.92      0.85      0.88        13
           2       0.86      0.92      0.89        13

   micro avg       0.93      0.93      0.93        45
   macro avg       0.92      0.92      0.92        45
weighted avg       0.93      0.93      0.93        45

[[19  0  0]
 [ 0 11  2]
 [ 0  1 12]]
</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div></div><div class="end_space"></div></div>
        <div id="tooltip" class="ipython_tooltip" style="left: 143.875px; top: 1306.26px; display: none;"><div class="tooltipbuttons"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" role="button" class="ui-button"><span class="ui-icon ui-icon-close">Close</span></a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="ui-corner-all" role="button" id="expanbutton" title="Grow the tooltip vertically (press shift-tab twice)" style=""><span class="ui-icon ui-icon-plus">Expand</span></a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" role="button" class="ui-button" title="show the current docstring in pager (press shift-tab 4 times)"><span class="ui-icon ui-icon-arrowstop-l-n">Open in Pager</span></a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" role="button" class="ui-button" title="Tooltip will linger for 10 seconds while you type" style="display: none;"><span class="ui-icon ui-icon-clock">Close</span></a></div><div class="pretooltiparrow" style="left: 204.778px;"></div><div class="tooltiptext smalltooltip"><pre><span class="ansi-red-intense-fg ansi-bold">Signature:</span> scaler<span class="ansi-yellow-intense-fg ansi-bold">.</span>transform<span class="ansi-yellow-intense-fg ansi-bold">(</span>X<span class="ansi-yellow-intense-fg ansi-bold">,</span> y<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-blue-intense-fg ansi-bold">'deprecated'</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> copy<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">)</span>
<span class="ansi-red-intense-fg ansi-bold">Docstring:</span>
Perform standardization by centering and scaling

Parameters
----------
X : array-like, shape [n_samples, n_features]
    The data used to scale along the features axis.
y : (ignored)
    .. deprecated:: 0.19
       This parameter will be removed in 0.21.
copy : bool, optional (default: None)
    Copy the input X or not.
<span class="ansi-red-intense-fg ansi-bold">File:</span>      c:\users\stevy\anaconda3\lib\site-packages\sklearn\preprocessing\data.py
<span class="ansi-red-intense-fg ansi-bold">Type:</span>      method
</pre></div></div>
    </div>
</div>



</div>



<div id="pager" class="ui-resizable">
    <div id="pager-contents">
        <div id="pager-container" class="container"></div>
    </div>
    <div id="pager-button-area"><a role="button" title="Open the pager in an external window" class="ui-button"><span class="ui-icon ui-icon-extlink"></span></a><a role="button" title="Close the pager" class="ui-button"><span class="ui-icon ui-icon-close"></span></a></div>
<div class="ui-resizable-handle ui-resizable-n" style="z-index: 90;"></div></div>






<script type="text/javascript">
    sys_info = {"notebook_version": "5.6.0", "notebook_path": "C:\\Users\\Stevy\\Anaconda3\\lib\\site-packages\\notebook", "commit_source": "", "commit_hash": "", "sys_version": "3.7.0 (default, Jun 28 2018, 08:04:48) [MSC v.1912 64 bit (AMD64)]", "sys_executable": "C:\\Users\\Stevy\\Anaconda3\\python.exe", "sys_platform": "win32", "platform": "Windows-10-10.0.17134-SP0", "os_name": "nt", "default_encoding": "utf-8"};
</script>

<script src="./README_files/encoding.js.download" charset="utf-8"></script>

<script src="./README_files/main.min.js.download" type="text/javascript" charset="utf-8"></script>



<script type="text/javascript">
  function _remove_token_from_url() {
    if (window.location.search.length <= 1) {
      return;
    }
    var search_parameters = window.location.search.slice(1).split('&');
    for (var i = 0; i < search_parameters.length; i++) {
      if (search_parameters[i].split('=')[0] === 'token') {
        // remote token from search parameters
        search_parameters.splice(i, 1);
        var new_search = '';
        if (search_parameters.length) {
          new_search = '?' + search_parameters.join('&');
        }
        var new_url = window.location.origin + 
                      window.location.pathname + 
                      new_search + 
                      window.location.hash;
        window.history.replaceState({}, "", new_url);
        return;
      }
    }
  }
  _remove_token_from_url();
</script>


<div style="position: absolute; width: 0px; height: 0px; overflow: hidden; padding: 0px; border: 0px; margin: 0px;"><div id="MathJax_Font_Test" style="position: absolute; visibility: hidden; top: 0px; left: 0px; width: auto; min-width: 0px; max-width: none; padding: 0px; border: 0px; margin: 0px; white-space: nowrap; text-align: left; text-indent: 0px; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; font-size: 40px; font-weight: normal; font-style: normal; font-family: STIXMathJax_Main, sans-serif;"></div></div><div id="varInspector-wrapper" style="position: fixed; display: none; max-height: 731px;" class="ui-draggable ui-resizable varInspector-float-wrapper"><div id="varInspector-header" class="header">Variable Inspector <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="kill-btn" title="Close window">[x]</a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="hide-btn" title="Hide Variable Inspector">[-]</a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" class="reload-btn" title="Reload Variable Inspector">  ↻</a><span>&nbsp;&nbsp;</span><span>&nbsp;&nbsp;</span></div><div id="varInspector" class="varInspector" style="height: 92.222px; max-height: 711px;"><div class="inspector"><table class="table fixed table-condensed table-nonfluid tablesorter tablesorter-default" role="grid"><colgroup><col>  <col><col></colgroup><thead><tr role="row" class="tablesorter-headerRow"><th data-column="0" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="X: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">X</div></th><th data-column="1" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Name: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Name</div></th><th data-column="2" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Type: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Type</div></th><th data-column="3" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Size: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Size</div></th><th data-column="4" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Shape: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Shape</div></th><th data-column="5" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Value: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Value</div></th></tr></thead><tbody aria-live="polite" aria-relevant="all"><tr role="row"><td>  </td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del GridSearchCV&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>GridSearchCV</td><td>ABCMeta</td><td>1464</td><td></td><td><class 'sklearn.model_selection._sear...<="" td=""></class></td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del PCA&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>PCA</td><td>ABCMeta</td><td>1464</td><td></td><td><class 'sklearn.decomposition.pca.pca'=""></class></td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del SVC&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>SVC</td><td>ABCMeta</td><td>2000</td><td></td><td><class 'sklearn.svm.classes.svc'=""></class></td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del X&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>X</td><td>DataFrame</td><td>2480</td><td>(150, 2)</td><td>          PC1       PC2
0   -2.264703...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del X_test&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>X_test</td><td>DataFrame</td><td>1080</td><td>(45, 2)</td><td>          PC1       PC2
73   0.632858...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del X_train&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>X_train</td><td>DataFrame</td><td>2520</td><td>(105, 2)</td><td>          PC1       PC2
81   0.023453...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del df&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>df</td><td>DataFrame</td><td>4880</td><td>(150, 4)</td><td>     sepal length (cm)  sepal width (...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del df_pca&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>df_pca</td><td>DataFrame</td><td>2480</td><td>(150, 2)</td><td>          PC1       PC2
0   -2.264703...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del df_pca_comp&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>df_pca_comp</td><td>DataFrame</td><td>144</td><td>(2, 4)</td><td>   sepal length (cm)  sepal width (cm...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del df_scaled&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>df_scaled</td><td>ndarray</td><td>4800</td><td>(150, 4)</td><td>[[-9.00681170e-01  1.01900435e+00 -1....</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del df_scaler&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>df_scaler</td><td>ndarray</td><td>4800</td><td>(150, 4)</td><td>[[-9.00681170e-01  1.01900435e+00 -1....</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del grid&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>grid</td><td>GridSearchCV</td><td>56</td><td></td><td>GridSearchCV(cv='warn', error_score='...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del grid_predictions&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>grid_predicti...</td><td>ndarray</td><td>180</td><td>(45,)</td><td>[1 0 2 1 2 0 1 2 2 1 2 0 0 0 0 1 2 1 ...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del iris&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>iris</td><td>Bunch</td><td>384</td><td></td><td>{'data': array([[5.1, 3.5, 1.4, 0.2],...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del model&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>model</td><td>SVC</td><td>56</td><td></td><td>SVC(C=1.0, cache_size=200, class_weig...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del param_grid&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>param_grid</td><td>dict</td><td>240</td><td></td><td>{'C': [0.01, 0.1, 10, 100, 1000], 'ga...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del pc12&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>pc12</td><td>ndarray</td><td>2400</td><td>(150, 2)</td><td>[[-2.26470281  0.4800266 ]
 [-2.08096...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del pca&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>pca</td><td>PCA</td><td>56</td><td></td><td>PCA(copy=True, iterated_power='auto',...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del predictions&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>predictions</td><td>ndarray</td><td>180</td><td>(45,)</td><td>[1 0 2 1 2 0 1 2 2 1 2 0 0 0 0 1 2 1 ...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del scaler&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>scaler</td><td>StandardScaler</td><td>56</td><td></td><td>StandardScaler(copy=True, with_mean=T...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del y&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>y</td><td>ndarray</td><td>600</td><td>(150,)</td><td>[0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 ...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del y_test&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>y_test</td><td>ndarray</td><td>180</td><td>(45,)</td><td>[1 0 2 1 1 0 1 2 1 1 2 0 0 0 0 1 2 1 ...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_16_PCA/Iris_Dataset_Project.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del y_train&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>y_train</td><td>ndarray</td><td>420</td><td>(105,)</td><td>[1 2 2 1 2 1 2 1 0 2 1 0 0 0 1 2 0 0 ...</td></tr></tbody></table></div></div><div class="ui-resizable-handle ui-resizable-e" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div></div><style>#toc li > span:hover { background-color: #DAA520 }
.toc-item-highlight-select  {background-color: #FFD700}
.toc-item-highlight-execute  {background-color: #FF0000}
.toc-item-highlight-execute.toc-item-highlight-select   {background-color: #FFD700}div#menubar-container, div#header-container {
width: auto;
padding-left: 20px; }#toc-wrapper { background-color: #FFFFFF}
#toc a, #navigate_menu a, .toc { color: #333333}#toc-wrapper .toc-item-num { color: #000000}.sidebar-wrapper { border-color: #EEEEEE}.highlight_on_scroll { border-left: solid 4px #2447f0}</style><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 1</strong>  <div title="jupyter-notebook:change-cell-to-heading-1" class="pull-right command-shortcut"><kbd>1</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 2</strong>  <div title="jupyter-notebook:change-cell-to-heading-2" class="pull-right command-shortcut"><kbd>2</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 1</strong>  <div title="jupyter-notebook:change-cell-to-heading-1" class="pull-right command-shortcut"><kbd>1</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 3</strong>  <div title="jupyter-notebook:change-cell-to-heading-3" class="pull-right command-shortcut"><kbd>3</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 2</strong>  <div title="jupyter-notebook:change-cell-to-heading-2" class="pull-right command-shortcut"><kbd>2</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 2</strong>  <div title="jupyter-notebook:change-cell-to-heading-2" class="pull-right command-shortcut"><kbd>2</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div></body></html>