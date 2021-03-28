---
layout: single
permalink: /bayes_opt_subsampled/
title: "subsampling_opt_src"
subscribe: true
--- 

<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>bayes_opt_subsampling</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>




<style type="text/css">
    pre { line-height: 125%; margin: 0; }
td.linenos pre { color: #000000; background-color: #f0f0f0; padding: 0 5px 0 5px; }
span.linenos { color: #000000; background-color: #f0f0f0; padding: 0 5px 0 5px; }
td.linenos pre.special { color: #000000; background-color: #ffffc0; padding: 0 5px 0 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding: 0 5px 0 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>



<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/*
 * Webkit scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar,
[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-corner {
  background: var(--jp-scrollbar-background-color);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-thumb {
  background: rgb(var(--jp-scrollbar-thumb-color));
  border: var(--jp-scrollbar-thumb-margin) solid transparent;
  background-clip: content-box;
  border-radius: var(--jp-scrollbar-thumb-radius);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-track:horizontal {
  border-left: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
  border-right: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-track:vertical {
  border-top: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
  border-bottom: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar */

[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar::-webkit-scrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar::-webkit-scrollbar,
[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-corner,
[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-corner {
  background-color: transparent;
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-thumb,
[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
  border: var(--jp-scrollbar-thumb-margin) solid transparent;
  background-clip: content-box;
  border-radius: var(--jp-scrollbar-thumb-radius);
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-track:horizontal {
  border-left: var(--jp-scrollbar-endpad) solid transparent;
  border-right: var(--jp-scrollbar-endpad) solid transparent;
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-track:vertical {
  border-top: var(--jp-scrollbar-endpad) solid transparent;
  border-bottom: var(--jp-scrollbar-endpad) solid transparent;
}

/*
 * Phosphor
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-Widget, /* </DEPRECATED> */
.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  cursor: default;
}


/* <DEPRECATED> */ .p-Widget.p-mod-hidden, /* </DEPRECATED> */
.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-CommandPalette, /* </DEPRECATED> */
.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-CommandPalette-search, /* </DEPRECATED> */
.lm-CommandPalette-search {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-content, /* </DEPRECATED> */
.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}


/* <DEPRECATED> */ .p-CommandPalette-header, /* </DEPRECATED> */
.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}


/* <DEPRECATED> */ .p-CommandPalette-item, /* </DEPRECATED> */
.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}


/* <DEPRECATED> */ .p-CommandPalette-itemIcon, /* </DEPRECATED> */
.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-itemContent, /* </DEPRECATED> */
.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}


/* <DEPRECATED> */ .p-CommandPalette-itemShortcut, /* </DEPRECATED> */
.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-itemLabel, /* </DEPRECATED> */
.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-DockPanel, /* </DEPRECATED> */
.lm-DockPanel {
  z-index: 0;
}


/* <DEPRECATED> */ .p-DockPanel-widget, /* </DEPRECATED> */
.lm-DockPanel-widget {
  z-index: 0;
}


/* <DEPRECATED> */ .p-DockPanel-tabBar, /* </DEPRECATED> */
.lm-DockPanel-tabBar {
  z-index: 1;
}


/* <DEPRECATED> */ .p-DockPanel-handle, /* </DEPRECATED> */
.lm-DockPanel-handle {
  z-index: 2;
}


/* <DEPRECATED> */ .p-DockPanel-handle.p-mod-hidden, /* </DEPRECATED> */
.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-DockPanel-handle:after, /* </DEPRECATED> */
.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='horizontal'],
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='vertical'],
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='horizontal']:after,
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='vertical']:after,
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}


/* <DEPRECATED> */ .p-DockPanel-overlay, /* </DEPRECATED> */
.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}


/* <DEPRECATED> */ .p-DockPanel-overlay.p-mod-hidden, /* </DEPRECATED> */
.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-Menu, /* </DEPRECATED> */
.lm-Menu {
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


/* <DEPRECATED> */ .p-Menu-content, /* </DEPRECATED> */
.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}


/* <DEPRECATED> */ .p-Menu-item, /* </DEPRECATED> */
.lm-Menu-item {
  display: table-row;
}


/* <DEPRECATED> */
.p-Menu-item.p-mod-hidden,
.p-Menu-item.p-mod-collapsed,
/* </DEPRECATED> */
.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}


/* <DEPRECATED> */
.p-Menu-itemIcon,
.p-Menu-itemSubmenuIcon,
/* </DEPRECATED> */
.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}


/* <DEPRECATED> */ .p-Menu-itemLabel, /* </DEPRECATED> */
.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}


/* <DEPRECATED> */ .p-Menu-itemShortcut, /* </DEPRECATED> */
.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-MenuBar, /* </DEPRECATED> */
.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-MenuBar-content, /* </DEPRECATED> */
.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}


/* <DEPRECATED> */ .p--MenuBar-item, /* </DEPRECATED> */
.lm-MenuBar-item {
  box-sizing: border-box;
}


/* <DEPRECATED> */
.p-MenuBar-itemIcon,
.p-MenuBar-itemLabel,
/* </DEPRECATED> */
.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-ScrollBar, /* </DEPRECATED> */
.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */
.p-ScrollBar[data-orientation='horizontal'],
/* </DEPRECATED> */
.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}


/* <DEPRECATED> */
.p-ScrollBar[data-orientation='vertical'],
/* </DEPRECATED> */
.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}


/* <DEPRECATED> */ .p-ScrollBar-button, /* </DEPRECATED> */
.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-ScrollBar-track, /* </DEPRECATED> */
.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}


/* <DEPRECATED> */ .p-ScrollBar-thumb, /* </DEPRECATED> */
.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-SplitPanel-child, /* </DEPRECATED> */
.lm-SplitPanel-child {
  z-index: 0;
}


/* <DEPRECATED> */ .p-SplitPanel-handle, /* </DEPRECATED> */
.lm-SplitPanel-handle {
  z-index: 1;
}


/* <DEPRECATED> */ .p-SplitPanel-handle.p-mod-hidden, /* </DEPRECATED> */
.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-SplitPanel-handle:after, /* </DEPRECATED> */
.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle:after,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle:after,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-TabBar, /* </DEPRECATED> */
.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-TabBar[data-orientation='horizontal'], /* </DEPRECATED> */
.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
}


/* <DEPRECATED> */ .p-TabBar[data-orientation='vertical'], /* </DEPRECATED> */
.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
}


/* <DEPRECATED> */ .p-TabBar-content, /* </DEPRECATED> */
.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}


/* <DEPRECATED> */
.p-TabBar[data-orientation='horizontal'] > .p-TabBar-content,
/* </DEPRECATED> */
.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}


/* <DEPRECATED> */
.p-TabBar[data-orientation='vertical'] > .p-TabBar-content,
/* </DEPRECATED> */
.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}


/* <DEPRECATED> */ .p-TabBar-tab, /* </DEPRECATED> */
.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
}


/* <DEPRECATED> */
.p-TabBar-tabIcon,
.p-TabBar-tabCloseIcon,
/* </DEPRECATED> */
.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-TabBar-tabLabel, /* </DEPRECATED> */
.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}


/* <DEPRECATED> */ .p-TabBar-tab.p-mod-hidden, /* </DEPRECATED> */
.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-TabBar.p-mod-dragging .p-TabBar-tab, /* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab,
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab,
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-TabPanel-tabBar, /* </DEPRECATED> */
.lm-TabPanel-tabBar {
  z-index: 1;
}


/* <DEPRECATED> */ .p-TabPanel-stackedPanel, /* </DEPRECATED> */
.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

@charset "UTF-8";
/*!

Copyright 2015-present Palantir Technologies, Inc. All rights reserved.
Licensed under the Apache License, Version 2.0.

*/
html{
  -webkit-box-sizing:border-box;
          box-sizing:border-box; }

*,
*::before,
*::after{
  -webkit-box-sizing:inherit;
          box-sizing:inherit; }

body{
  text-transform:none;
  line-height:1.28581;
  letter-spacing:0;
  font-size:14px;
  font-weight:400;
  color:#182026;
  font-family:-apple-system, "BlinkMacSystemFont", "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Open Sans", "Helvetica Neue", "Icons16", sans-serif; }

p{
  margin-top:0;
  margin-bottom:10px; }

small{
  font-size:12px; }

strong{
  font-weight:600; }

::-moz-selection{
  background:rgba(125, 188, 255, 0.6); }

::selection{
  background:rgba(125, 188, 255, 0.6); }
.bp3-heading{
  color:#182026;
  font-weight:600;
  margin:0 0 10px;
  padding:0; }
  .bp3-dark .bp3-heading{
    color:#f5f8fa; }

h1.bp3-heading, .bp3-running-text h1{
  line-height:40px;
  font-size:36px; }

h2.bp3-heading, .bp3-running-text h2{
  line-height:32px;
  font-size:28px; }

h3.bp3-heading, .bp3-running-text h3{
  line-height:25px;
  font-size:22px; }

h4.bp3-heading, .bp3-running-text h4{
  line-height:21px;
  font-size:18px; }

h5.bp3-heading, .bp3-running-text h5{
  line-height:19px;
  font-size:16px; }

h6.bp3-heading, .bp3-running-text h6{
  line-height:16px;
  font-size:14px; }
.bp3-ui-text{
  text-transform:none;
  line-height:1.28581;
  letter-spacing:0;
  font-size:14px;
  font-weight:400; }

.bp3-monospace-text{
  text-transform:none;
  font-family:monospace; }

.bp3-text-muted{
  color:#5c7080; }
  .bp3-dark .bp3-text-muted{
    color:#a7b6c2; }

.bp3-text-disabled{
  color:rgba(92, 112, 128, 0.6); }
  .bp3-dark .bp3-text-disabled{
    color:rgba(167, 182, 194, 0.6); }

.bp3-text-overflow-ellipsis{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal; }
.bp3-running-text{
  line-height:1.5;
  font-size:14px; }
  .bp3-running-text h1{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h1{
      color:#f5f8fa; }
  .bp3-running-text h2{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h2{
      color:#f5f8fa; }
  .bp3-running-text h3{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h3{
      color:#f5f8fa; }
  .bp3-running-text h4{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h4{
      color:#f5f8fa; }
  .bp3-running-text h5{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h5{
      color:#f5f8fa; }
  .bp3-running-text h6{
    color:#182026;
    font-weight:600;
    margin-top:40px;
    margin-bottom:20px; }
    .bp3-dark .bp3-running-text h6{
      color:#f5f8fa; }
  .bp3-running-text hr{
    margin:20px 0;
    border:none;
    border-bottom:1px solid rgba(16, 22, 26, 0.15); }
    .bp3-dark .bp3-running-text hr{
      border-color:rgba(255, 255, 255, 0.15); }
  .bp3-running-text p{
    margin:0 0 10px;
    padding:0; }

.bp3-text-large{
  font-size:16px; }

.bp3-text-small{
  font-size:12px; }
a{
  text-decoration:none;
  color:#106ba3; }
  a:hover{
    cursor:pointer;
    text-decoration:underline;
    color:#106ba3; }
  a .bp3-icon, a .bp3-icon-standard, a .bp3-icon-large{
    color:inherit; }
  a code,
  .bp3-dark a code{
    color:inherit; }
  .bp3-dark a,
  .bp3-dark a:hover{
    color:#48aff0; }
    .bp3-dark a .bp3-icon, .bp3-dark a .bp3-icon-standard, .bp3-dark a .bp3-icon-large,
    .bp3-dark a:hover .bp3-icon,
    .bp3-dark a:hover .bp3-icon-standard,
    .bp3-dark a:hover .bp3-icon-large{
      color:inherit; }
.bp3-running-text code, .bp3-code{
  text-transform:none;
  font-family:monospace;
  border-radius:3px;
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2);
  background:rgba(255, 255, 255, 0.7);
  padding:2px 5px;
  color:#5c7080;
  font-size:smaller; }
  .bp3-dark .bp3-running-text code, .bp3-running-text .bp3-dark code, .bp3-dark .bp3-code{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#a7b6c2; }
  .bp3-running-text a > code, a > .bp3-code{
    color:#137cbd; }
    .bp3-dark .bp3-running-text a > code, .bp3-running-text .bp3-dark a > code, .bp3-dark a > .bp3-code{
      color:inherit; }

.bp3-running-text pre, .bp3-code-block{
  text-transform:none;
  font-family:monospace;
  display:block;
  margin:10px 0;
  border-radius:3px;
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
  background:rgba(255, 255, 255, 0.7);
  padding:13px 15px 12px;
  line-height:1.4;
  color:#182026;
  font-size:13px;
  word-break:break-all;
  word-wrap:break-word; }
  .bp3-dark .bp3-running-text pre, .bp3-running-text .bp3-dark pre, .bp3-dark .bp3-code-block{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#f5f8fa; }
  .bp3-running-text pre > code, .bp3-code-block > code{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:none;
    padding:0;
    color:inherit;
    font-size:inherit; }

.bp3-running-text kbd, .bp3-key{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  background:#ffffff;
  min-width:24px;
  height:24px;
  padding:3px 6px;
  vertical-align:middle;
  line-height:24px;
  color:#5c7080;
  font-family:inherit;
  font-size:12px; }
  .bp3-running-text kbd .bp3-icon, .bp3-key .bp3-icon, .bp3-running-text kbd .bp3-icon-standard, .bp3-key .bp3-icon-standard, .bp3-running-text kbd .bp3-icon-large, .bp3-key .bp3-icon-large{
    margin-right:5px; }
  .bp3-dark .bp3-running-text kbd, .bp3-running-text .bp3-dark kbd, .bp3-dark .bp3-key{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
    background:#394b59;
    color:#a7b6c2; }
.bp3-running-text blockquote, .bp3-blockquote{
  margin:0 0 10px;
  border-left:solid 4px rgba(167, 182, 194, 0.5);
  padding:0 20px; }
  .bp3-dark .bp3-running-text blockquote, .bp3-running-text .bp3-dark blockquote, .bp3-dark .bp3-blockquote{
    border-color:rgba(115, 134, 148, 0.5); }
.bp3-running-text ul,
.bp3-running-text ol, .bp3-list{
  margin:10px 0;
  padding-left:30px; }
  .bp3-running-text ul li:not(:last-child), .bp3-running-text ol li:not(:last-child), .bp3-list li:not(:last-child){
    margin-bottom:5px; }
  .bp3-running-text ul ol, .bp3-running-text ol ol, .bp3-list ol,
  .bp3-running-text ul ul,
  .bp3-running-text ol ul,
  .bp3-list ul{
    margin-top:5px; }

.bp3-list-unstyled{
  margin:0;
  padding:0;
  list-style:none; }
  .bp3-list-unstyled li{
    padding:0; }
.bp3-rtl{
  text-align:right; }

.bp3-dark{
  color:#f5f8fa; }

:focus{
  outline:rgba(19, 124, 189, 0.6) auto 2px;
  outline-offset:2px;
  -moz-outline-radius:6px; }

.bp3-focus-disabled :focus{
  outline:none !important; }
  .bp3-focus-disabled :focus ~ .bp3-control-indicator{
    outline:none !important; }

.bp3-alert{
  max-width:400px;
  padding:20px; }

.bp3-alert-body{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex; }
  .bp3-alert-body .bp3-icon{
    margin-top:0;
    margin-right:20px;
    font-size:40px; }

.bp3-alert-footer{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:reverse;
      -ms-flex-direction:row-reverse;
          flex-direction:row-reverse;
  margin-top:10px; }
  .bp3-alert-footer .bp3-button{
    margin-left:10px; }
.bp3-breadcrumbs{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-wrap:wrap;
      flex-wrap:wrap;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  margin:0;
  cursor:default;
  height:30px;
  padding:0;
  list-style:none; }
  .bp3-breadcrumbs > li{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center; }
    .bp3-breadcrumbs > li::after{
      display:block;
      margin:0 5px;
      background:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M10.71 7.29l-4-4a1.003 1.003 0 0 0-1.42 1.42L8.59 8 5.3 11.29c-.19.18-.3.43-.3.71a1.003 1.003 0 0 0 1.71.71l4-4c.18-.18.29-.43.29-.71 0-.28-.11-.53-.29-.71z' fill='%235C7080'/%3e%3c/svg%3e");
      width:16px;
      height:16px;
      content:""; }
    .bp3-breadcrumbs > li:last-of-type::after{
      display:none; }

.bp3-breadcrumb,
.bp3-breadcrumb-current,
.bp3-breadcrumbs-collapsed{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  font-size:16px; }

.bp3-breadcrumb,
.bp3-breadcrumbs-collapsed{
  color:#5c7080; }

.bp3-breadcrumb:hover{
  text-decoration:none; }

.bp3-breadcrumb.bp3-disabled{
  cursor:not-allowed;
  color:rgba(92, 112, 128, 0.6); }

.bp3-breadcrumb .bp3-icon{
  margin-right:5px; }

.bp3-breadcrumb-current{
  color:inherit;
  font-weight:600; }
  .bp3-breadcrumb-current .bp3-input{
    vertical-align:baseline;
    font-size:inherit;
    font-weight:inherit; }

.bp3-breadcrumbs-collapsed{
  margin-right:2px;
  border:none;
  border-radius:3px;
  background:#ced9e0;
  cursor:pointer;
  padding:1px 5px;
  vertical-align:text-bottom; }
  .bp3-breadcrumbs-collapsed::before{
    display:block;
    background:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cg fill='%235C7080'%3e%3ccircle cx='2' cy='8.03' r='2'/%3e%3ccircle cx='14' cy='8.03' r='2'/%3e%3ccircle cx='8' cy='8.03' r='2'/%3e%3c/g%3e%3c/svg%3e") center no-repeat;
    width:16px;
    height:16px;
    content:""; }
  .bp3-breadcrumbs-collapsed:hover{
    background:#bfccd6;
    text-decoration:none;
    color:#182026; }

.bp3-dark .bp3-breadcrumb,
.bp3-dark .bp3-breadcrumbs-collapsed{
  color:#a7b6c2; }

.bp3-dark .bp3-breadcrumbs > li::after{
  color:#a7b6c2; }

.bp3-dark .bp3-breadcrumb.bp3-disabled{
  color:rgba(167, 182, 194, 0.6); }

.bp3-dark .bp3-breadcrumb-current{
  color:#f5f8fa; }

.bp3-dark .bp3-breadcrumbs-collapsed{
  background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-breadcrumbs-collapsed:hover{
    background:rgba(16, 22, 26, 0.6);
    color:#f5f8fa; }
.bp3-button{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  border:none;
  border-radius:3px;
  cursor:pointer;
  padding:5px 10px;
  vertical-align:middle;
  text-align:left;
  font-size:14px;
  min-width:30px;
  min-height:30px; }
  .bp3-button > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-button > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-button::before,
  .bp3-button > *{
    margin-right:7px; }
  .bp3-button:empty::before,
  .bp3-button > :last-child{
    margin-right:0; }
  .bp3-button:empty{
    padding:0 !important; }
  .bp3-button:disabled, .bp3-button.bp3-disabled{
    cursor:not-allowed; }
  .bp3-button.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-button.bp3-align-right,
  .bp3-align-right .bp3-button{
    text-align:right; }
  .bp3-button.bp3-align-left,
  .bp3-align-left .bp3-button{
    text-align:left; }
  .bp3-button:not([class*="bp3-intent-"]){
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    color:#182026; }
    .bp3-button:not([class*="bp3-intent-"]):hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
      background-clip:padding-box;
      background-color:#ebf1f5; }
    .bp3-button:not([class*="bp3-intent-"]):active, .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#d8e1e8;
      background-image:none; }
    .bp3-button:not([class*="bp3-intent-"]):disabled, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled{
      outline:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(206, 217, 224, 0.5);
      background-image:none;
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6); }
      .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active, .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active:hover, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active:hover{
        background:rgba(206, 217, 224, 0.7); }
  .bp3-button.bp3-intent-primary{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
    .bp3-button.bp3-intent-primary:hover, .bp3-button.bp3-intent-primary:active, .bp3-button.bp3-intent-primary.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-primary:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
      background-color:#106ba3; }
    .bp3-button.bp3-intent-primary:active, .bp3-button.bp3-intent-primary.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#0e5a8a;
      background-image:none; }
    .bp3-button.bp3-intent-primary:disabled, .bp3-button.bp3-intent-primary.bp3-disabled{
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(19, 124, 189, 0.5);
      background-image:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-success{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#0f9960;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
    .bp3-button.bp3-intent-success:hover, .bp3-button.bp3-intent-success:active, .bp3-button.bp3-intent-success.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-success:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
      background-color:#0d8050; }
    .bp3-button.bp3-intent-success:active, .bp3-button.bp3-intent-success.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#0a6640;
      background-image:none; }
    .bp3-button.bp3-intent-success:disabled, .bp3-button.bp3-intent-success.bp3-disabled{
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(15, 153, 96, 0.5);
      background-image:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-warning{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#d9822b;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
    .bp3-button.bp3-intent-warning:hover, .bp3-button.bp3-intent-warning:active, .bp3-button.bp3-intent-warning.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-warning:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
      background-color:#bf7326; }
    .bp3-button.bp3-intent-warning:active, .bp3-button.bp3-intent-warning.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#a66321;
      background-image:none; }
    .bp3-button.bp3-intent-warning:disabled, .bp3-button.bp3-intent-warning.bp3-disabled{
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(217, 130, 43, 0.5);
      background-image:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-danger{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#db3737;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
    .bp3-button.bp3-intent-danger:hover, .bp3-button.bp3-intent-danger:active, .bp3-button.bp3-intent-danger.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-danger:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
      background-color:#c23030; }
    .bp3-button.bp3-intent-danger:active, .bp3-button.bp3-intent-danger.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#a82a2a;
      background-image:none; }
    .bp3-button.bp3-intent-danger:disabled, .bp3-button.bp3-intent-danger.bp3-disabled{
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(219, 55, 55, 0.5);
      background-image:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button[class*="bp3-intent-"] .bp3-button-spinner .bp3-spinner-head{
    stroke:#ffffff; }
  .bp3-button.bp3-large,
  .bp3-large .bp3-button{
    min-width:40px;
    min-height:40px;
    padding:5px 15px;
    font-size:16px; }
    .bp3-button.bp3-large::before,
    .bp3-button.bp3-large > *,
    .bp3-large .bp3-button::before,
    .bp3-large .bp3-button > *{
      margin-right:10px; }
    .bp3-button.bp3-large:empty::before,
    .bp3-button.bp3-large > :last-child,
    .bp3-large .bp3-button:empty::before,
    .bp3-large .bp3-button > :last-child{
      margin-right:0; }
  .bp3-button.bp3-small,
  .bp3-small .bp3-button{
    min-width:24px;
    min-height:24px;
    padding:0 7px; }
  .bp3-button.bp3-loading{
    position:relative; }
    .bp3-button.bp3-loading[class*="bp3-icon-"]::before{
      visibility:hidden; }
    .bp3-button.bp3-loading .bp3-button-spinner{
      position:absolute;
      margin:0; }
    .bp3-button.bp3-loading > :not(.bp3-button-spinner){
      visibility:hidden; }
  .bp3-button[class*="bp3-icon-"]::before{
    line-height:1;
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-weight:400;
    font-style:normal;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    color:#5c7080; }
  .bp3-button .bp3-icon, .bp3-button .bp3-icon-standard, .bp3-button .bp3-icon-large{
    color:#5c7080; }
    .bp3-button .bp3-icon.bp3-align-right, .bp3-button .bp3-icon-standard.bp3-align-right, .bp3-button .bp3-icon-large.bp3-align-right{
      margin-left:7px; }
  .bp3-button .bp3-icon:first-child:last-child,
  .bp3-button .bp3-spinner + .bp3-icon:last-child{
    margin:0 -7px; }
  .bp3-dark .bp3-button:not([class*="bp3-intent-"]){
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#394b59;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
    color:#f5f8fa; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):hover, .bp3-dark .bp3-button:not([class*="bp3-intent-"]):active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      color:#f5f8fa; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):hover{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#30404d; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#202b33;
      background-image:none; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):disabled, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(57, 75, 89, 0.5);
      background-image:none;
      color:rgba(167, 182, 194, 0.6); }
      .bp3-dark .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active{
        background:rgba(57, 75, 89, 0.7); }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-button-spinner .bp3-spinner-head{
      background:rgba(16, 22, 26, 0.5);
      stroke:#8a9ba8; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"])[class*="bp3-icon-"]::before{
      color:#a7b6c2; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon, .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon-standard, .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon-large{
      color:#a7b6c2; }
  .bp3-dark .bp3-button[class*="bp3-intent-"]{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:hover{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:active, .bp3-dark .bp3-button[class*="bp3-intent-"].bp3-active{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:disabled, .bp3-dark .bp3-button[class*="bp3-intent-"].bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background-image:none;
      color:rgba(255, 255, 255, 0.3); }
    .bp3-dark .bp3-button[class*="bp3-intent-"] .bp3-button-spinner .bp3-spinner-head{
      stroke:#8a9ba8; }
  .bp3-button:disabled::before,
  .bp3-button:disabled .bp3-icon, .bp3-button:disabled .bp3-icon-standard, .bp3-button:disabled .bp3-icon-large, .bp3-button.bp3-disabled::before,
  .bp3-button.bp3-disabled .bp3-icon, .bp3-button.bp3-disabled .bp3-icon-standard, .bp3-button.bp3-disabled .bp3-icon-large, .bp3-button[class*="bp3-intent-"]::before,
  .bp3-button[class*="bp3-intent-"] .bp3-icon, .bp3-button[class*="bp3-intent-"] .bp3-icon-standard, .bp3-button[class*="bp3-intent-"] .bp3-icon-large{
    color:inherit !important; }
  .bp3-button.bp3-minimal{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:none; }
    .bp3-button.bp3-minimal:hover{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(167, 182, 194, 0.3);
      text-decoration:none;
      color:#182026; }
    .bp3-button.bp3-minimal:active, .bp3-button.bp3-minimal.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(115, 134, 148, 0.3);
      color:#182026; }
    .bp3-button.bp3-minimal:disabled, .bp3-button.bp3-minimal:disabled:hover, .bp3-button.bp3-minimal.bp3-disabled, .bp3-button.bp3-minimal.bp3-disabled:hover{
      background:none;
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6); }
      .bp3-button.bp3-minimal:disabled.bp3-active, .bp3-button.bp3-minimal:disabled:hover.bp3-active, .bp3-button.bp3-minimal.bp3-disabled.bp3-active, .bp3-button.bp3-minimal.bp3-disabled:hover.bp3-active{
        background:rgba(115, 134, 148, 0.3); }
    .bp3-dark .bp3-button.bp3-minimal{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:inherit; }
      .bp3-dark .bp3-button.bp3-minimal:hover, .bp3-dark .bp3-button.bp3-minimal:active, .bp3-dark .bp3-button.bp3-minimal.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none; }
      .bp3-dark .bp3-button.bp3-minimal:hover{
        background:rgba(138, 155, 168, 0.15); }
      .bp3-dark .bp3-button.bp3-minimal:active, .bp3-dark .bp3-button.bp3-minimal.bp3-active{
        background:rgba(138, 155, 168, 0.3);
        color:#f5f8fa; }
      .bp3-dark .bp3-button.bp3-minimal:disabled, .bp3-dark .bp3-button.bp3-minimal:disabled:hover, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled:hover{
        background:none;
        cursor:not-allowed;
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-button.bp3-minimal:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal:disabled:hover.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled:hover.bp3-active{
          background:rgba(138, 155, 168, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-primary{
      color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:hover, .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.15);
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:disabled, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(16, 107, 163, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-primary:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
        stroke:#106ba3; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary{
        color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:hover{
          background:rgba(19, 124, 189, 0.2);
          color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
          background:rgba(19, 124, 189, 0.3);
          color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled{
          background:none;
          color:rgba(72, 175, 240, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled.bp3-active{
            background:rgba(19, 124, 189, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-success{
      color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:hover, .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.15);
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:disabled, .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(13, 128, 80, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-success:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
        stroke:#0d8050; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success{
        color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:hover{
          background:rgba(15, 153, 96, 0.2);
          color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
          background:rgba(15, 153, 96, 0.3);
          color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled{
          background:none;
          color:rgba(61, 204, 145, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled.bp3-active{
            background:rgba(15, 153, 96, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-warning{
      color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:hover, .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.15);
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:disabled, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(191, 115, 38, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-warning:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
        stroke:#bf7326; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning{
        color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:hover{
          background:rgba(217, 130, 43, 0.2);
          color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
          background:rgba(217, 130, 43, 0.3);
          color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled{
          background:none;
          color:rgba(255, 179, 102, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled.bp3-active{
            background:rgba(217, 130, 43, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-danger{
      color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:hover, .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.15);
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:disabled, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(194, 48, 48, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-danger:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
        stroke:#c23030; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger{
        color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:hover{
          background:rgba(219, 55, 55, 0.2);
          color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
          background:rgba(219, 55, 55, 0.3);
          color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled{
          background:none;
          color:rgba(255, 115, 115, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled.bp3-active{
            background:rgba(219, 55, 55, 0.3); }

a.bp3-button{
  text-align:center;
  text-decoration:none;
  -webkit-transition:none;
  transition:none; }
  a.bp3-button, a.bp3-button:hover, a.bp3-button:active{
    color:#182026; }
  a.bp3-button.bp3-disabled{
    color:rgba(92, 112, 128, 0.6); }

.bp3-button-text{
  -webkit-box-flex:0;
      -ms-flex:0 1 auto;
          flex:0 1 auto; }

.bp3-button.bp3-align-left .bp3-button-text, .bp3-button.bp3-align-right .bp3-button-text,
.bp3-button-group.bp3-align-left .bp3-button-text,
.bp3-button-group.bp3-align-right .bp3-button-text{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto; }
.bp3-button-group{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex; }
  .bp3-button-group .bp3-button{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    position:relative;
    z-index:4; }
    .bp3-button-group .bp3-button:focus{
      z-index:5; }
    .bp3-button-group .bp3-button:hover{
      z-index:6; }
    .bp3-button-group .bp3-button:active, .bp3-button-group .bp3-button.bp3-active{
      z-index:7; }
    .bp3-button-group .bp3-button:disabled, .bp3-button-group .bp3-button.bp3-disabled{
      z-index:3; }
    .bp3-button-group .bp3-button[class*="bp3-intent-"]{
      z-index:9; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:focus{
        z-index:10; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:hover{
        z-index:11; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:active, .bp3-button-group .bp3-button[class*="bp3-intent-"].bp3-active{
        z-index:12; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:disabled, .bp3-button-group .bp3-button[class*="bp3-intent-"].bp3-disabled{
        z-index:8; }
  .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:first-child) .bp3-button,
  .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:first-child){
    border-top-left-radius:0;
    border-bottom-left-radius:0; }
  .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:last-child){
    margin-right:-1px;
    border-top-right-radius:0;
    border-bottom-right-radius:0; }
  .bp3-button-group.bp3-minimal .bp3-button{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:none; }
    .bp3-button-group.bp3-minimal .bp3-button:hover{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(167, 182, 194, 0.3);
      text-decoration:none;
      color:#182026; }
    .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(115, 134, 148, 0.3);
      color:#182026; }
    .bp3-button-group.bp3-minimal .bp3-button:disabled, .bp3-button-group.bp3-minimal .bp3-button:disabled:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover{
      background:none;
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6); }
      .bp3-button-group.bp3-minimal .bp3-button:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button:disabled:hover.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover.bp3-active{
        background:rgba(115, 134, 148, 0.3); }
    .bp3-dark .bp3-button-group.bp3-minimal .bp3-button{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:inherit; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:hover, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:hover{
        background:rgba(138, 155, 168, 0.15); }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
        background:rgba(138, 155, 168, 0.3);
        color:#f5f8fa; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled:hover, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover{
        background:none;
        cursor:not-allowed;
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled:hover.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover.bp3-active{
          background:rgba(138, 155, 168, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary{
      color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.15);
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(16, 107, 163, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
        stroke:#106ba3; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary{
        color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover{
          background:rgba(19, 124, 189, 0.2);
          color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
          background:rgba(19, 124, 189, 0.3);
          color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled{
          background:none;
          color:rgba(72, 175, 240, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled.bp3-active{
            background:rgba(19, 124, 189, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success{
      color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.15);
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(13, 128, 80, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
        stroke:#0d8050; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success{
        color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover{
          background:rgba(15, 153, 96, 0.2);
          color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
          background:rgba(15, 153, 96, 0.3);
          color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled{
          background:none;
          color:rgba(61, 204, 145, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled.bp3-active{
            background:rgba(15, 153, 96, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning{
      color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.15);
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(191, 115, 38, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
        stroke:#bf7326; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning{
        color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover{
          background:rgba(217, 130, 43, 0.2);
          color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
          background:rgba(217, 130, 43, 0.3);
          color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled{
          background:none;
          color:rgba(255, 179, 102, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled.bp3-active{
            background:rgba(217, 130, 43, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger{
      color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:none;
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.15);
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(194, 48, 48, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
        stroke:#c23030; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger{
        color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover{
          background:rgba(219, 55, 55, 0.2);
          color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
          background:rgba(219, 55, 55, 0.3);
          color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled{
          background:none;
          color:rgba(255, 115, 115, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled.bp3-active{
            background:rgba(219, 55, 55, 0.3); }
  .bp3-button-group .bp3-popover-wrapper,
  .bp3-button-group .bp3-popover-target{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-button-group.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-button-group .bp3-button.bp3-fill,
  .bp3-button-group.bp3-fill .bp3-button:not(.bp3-fixed){
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-button-group.bp3-vertical{
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column;
    -webkit-box-align:stretch;
        -ms-flex-align:stretch;
            align-items:stretch;
    vertical-align:top; }
    .bp3-button-group.bp3-vertical.bp3-fill{
      width:unset;
      height:100%; }
    .bp3-button-group.bp3-vertical .bp3-button{
      margin-right:0 !important;
      width:100%; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:first-child .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:first-child{
      border-radius:3px 3px 0 0; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:last-child .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:last-child{
      border-radius:0 0 3px 3px; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:not(:last-child){
      margin-bottom:-1px; }
  .bp3-button-group.bp3-align-left .bp3-button{
    text-align:left; }
  .bp3-dark .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-dark .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:last-child){
    margin-right:1px; }
  .bp3-dark .bp3-button-group.bp3-vertical > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-dark .bp3-button-group.bp3-vertical > .bp3-button:not(:last-child){
    margin-bottom:1px; }
.bp3-callout{
  line-height:1.5;
  font-size:14px;
  position:relative;
  border-radius:3px;
  background-color:rgba(138, 155, 168, 0.15);
  width:100%;
  padding:10px 12px 9px; }
  .bp3-callout[class*="bp3-icon-"]{
    padding-left:40px; }
    .bp3-callout[class*="bp3-icon-"]::before{
      line-height:1;
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-weight:400;
      font-style:normal;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased;
      position:absolute;
      top:10px;
      left:10px;
      color:#5c7080; }
  .bp3-callout.bp3-callout-icon{
    padding-left:40px; }
    .bp3-callout.bp3-callout-icon > .bp3-icon:first-child{
      position:absolute;
      top:10px;
      left:10px;
      color:#5c7080; }
  .bp3-callout .bp3-heading{
    margin-top:0;
    margin-bottom:5px;
    line-height:20px; }
    .bp3-callout .bp3-heading:last-child{
      margin-bottom:0; }
  .bp3-dark .bp3-callout{
    background-color:rgba(138, 155, 168, 0.2); }
    .bp3-dark .bp3-callout[class*="bp3-icon-"]::before{
      color:#a7b6c2; }
  .bp3-callout.bp3-intent-primary{
    background-color:rgba(19, 124, 189, 0.15); }
    .bp3-callout.bp3-intent-primary[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-primary > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-primary .bp3-heading{
      color:#106ba3; }
    .bp3-dark .bp3-callout.bp3-intent-primary{
      background-color:rgba(19, 124, 189, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-primary[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-primary > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-primary .bp3-heading{
        color:#48aff0; }
  .bp3-callout.bp3-intent-success{
    background-color:rgba(15, 153, 96, 0.15); }
    .bp3-callout.bp3-intent-success[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-success > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-success .bp3-heading{
      color:#0d8050; }
    .bp3-dark .bp3-callout.bp3-intent-success{
      background-color:rgba(15, 153, 96, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-success[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-success > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-success .bp3-heading{
        color:#3dcc91; }
  .bp3-callout.bp3-intent-warning{
    background-color:rgba(217, 130, 43, 0.15); }
    .bp3-callout.bp3-intent-warning[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-warning > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-warning .bp3-heading{
      color:#bf7326; }
    .bp3-dark .bp3-callout.bp3-intent-warning{
      background-color:rgba(217, 130, 43, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-warning[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-warning > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-warning .bp3-heading{
        color:#ffb366; }
  .bp3-callout.bp3-intent-danger{
    background-color:rgba(219, 55, 55, 0.15); }
    .bp3-callout.bp3-intent-danger[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-danger > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-danger .bp3-heading{
      color:#c23030; }
    .bp3-dark .bp3-callout.bp3-intent-danger{
      background-color:rgba(219, 55, 55, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-danger[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-danger > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-danger .bp3-heading{
        color:#ff7373; }
  .bp3-running-text .bp3-callout{
    margin:20px 0; }
.bp3-card{
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
  background-color:#ffffff;
  padding:20px;
  -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-card.bp3-dark,
  .bp3-dark .bp3-card{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
    background-color:#30404d; }

.bp3-elevation-0{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0); }
  .bp3-elevation-0.bp3-dark,
  .bp3-dark .bp3-elevation-0{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0); }

.bp3-elevation-1{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-1.bp3-dark,
  .bp3-dark .bp3-elevation-1{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-elevation-2{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 1px 1px rgba(16, 22, 26, 0.2), 0 2px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 1px 1px rgba(16, 22, 26, 0.2), 0 2px 6px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-2.bp3-dark,
  .bp3-dark .bp3-elevation-2{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.4), 0 2px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.4), 0 2px 6px rgba(16, 22, 26, 0.4); }

.bp3-elevation-3{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-3.bp3-dark,
  .bp3-dark .bp3-elevation-3{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }

.bp3-elevation-4{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-4.bp3-dark,
  .bp3-dark .bp3-elevation-4{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4); }

.bp3-card.bp3-interactive:hover{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  cursor:pointer; }
  .bp3-card.bp3-interactive:hover.bp3-dark,
  .bp3-dark .bp3-card.bp3-interactive:hover{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }

.bp3-card.bp3-interactive:active{
  opacity:0.9;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  -webkit-transition-duration:0;
          transition-duration:0; }
  .bp3-card.bp3-interactive:active.bp3-dark,
  .bp3-dark .bp3-card.bp3-interactive:active{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-collapse{
  height:0;
  overflow-y:hidden;
  -webkit-transition:height 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:height 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-collapse .bp3-collapse-body{
    -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-collapse .bp3-collapse-body[aria-hidden="true"]{
      display:none; }

.bp3-context-menu .bp3-popover-target{
  display:block; }

.bp3-context-menu-popover-target{
  position:fixed; }

.bp3-divider{
  margin:5px;
  border-right:1px solid rgba(16, 22, 26, 0.15);
  border-bottom:1px solid rgba(16, 22, 26, 0.15); }
  .bp3-dark .bp3-divider{
    border-color:rgba(16, 22, 26, 0.4); }
.bp3-dialog-container{
  opacity:1;
  -webkit-transform:scale(1);
          transform:scale(1);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  width:100%;
  min-height:100%;
  pointer-events:none;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-dialog-container.bp3-overlay-enter > .bp3-dialog, .bp3-dialog-container.bp3-overlay-appear > .bp3-dialog{
    opacity:0;
    -webkit-transform:scale(0.5);
            transform:scale(0.5); }
  .bp3-dialog-container.bp3-overlay-enter-active > .bp3-dialog, .bp3-dialog-container.bp3-overlay-appear-active > .bp3-dialog{
    opacity:1;
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-property:opacity, -webkit-transform;
    transition-property:opacity, -webkit-transform;
    transition-property:opacity, transform;
    transition-property:opacity, transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-dialog-container.bp3-overlay-exit > .bp3-dialog{
    opacity:1;
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-dialog-container.bp3-overlay-exit-active > .bp3-dialog{
    opacity:0;
    -webkit-transform:scale(0.5);
            transform:scale(0.5);
    -webkit-transition-property:opacity, -webkit-transform;
    transition-property:opacity, -webkit-transform;
    transition-property:opacity, transform;
    transition-property:opacity, transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }

.bp3-dialog{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:30px 0;
  border-radius:6px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  background:#ebf1f5;
  width:500px;
  padding-bottom:20px;
  pointer-events:all;
  -webkit-user-select:text;
     -moz-user-select:text;
      -ms-user-select:text;
          user-select:text; }
  .bp3-dialog:focus{
    outline:0; }
  .bp3-dialog.bp3-dark,
  .bp3-dark .bp3-dialog{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
    background:#293742;
    color:#f5f8fa; }

.bp3-dialog-header{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  border-radius:6px 6px 0 0;
  -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
  background:#ffffff;
  min-height:40px;
  padding-right:5px;
  padding-left:20px; }
  .bp3-dialog-header .bp3-icon-large,
  .bp3-dialog-header .bp3-icon{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    margin-right:10px;
    color:#5c7080; }
  .bp3-dialog-header .bp3-heading{
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    margin:0;
    line-height:inherit; }
    .bp3-dialog-header .bp3-heading:last-child{
      margin-right:20px; }
  .bp3-dark .bp3-dialog-header{
    -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:0 1px 0 rgba(16, 22, 26, 0.4);
    background:#30404d; }
    .bp3-dark .bp3-dialog-header .bp3-icon-large,
    .bp3-dark .bp3-dialog-header .bp3-icon{
      color:#a7b6c2; }

.bp3-dialog-body{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  margin:20px;
  line-height:18px; }

.bp3-dialog-footer{
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  margin:0 20px; }

.bp3-dialog-footer-actions{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-pack:end;
      -ms-flex-pack:end;
          justify-content:flex-end; }
  .bp3-dialog-footer-actions .bp3-button{
    margin-left:10px; }
.bp3-drawer{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:0;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  background:#ffffff;
  padding:0; }
  .bp3-drawer:focus{
    outline:0; }
  .bp3-drawer.bp3-position-top{
    top:0;
    right:0;
    left:0;
    height:50%; }
    .bp3-drawer.bp3-position-top.bp3-overlay-enter, .bp3-drawer.bp3-position-top.bp3-overlay-appear{
      -webkit-transform:translateY(-100%);
              transform:translateY(-100%); }
    .bp3-drawer.bp3-position-top.bp3-overlay-enter-active, .bp3-drawer.bp3-position-top.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer.bp3-position-top.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer.bp3-position-top.bp3-overlay-exit-active{
      -webkit-transform:translateY(-100%);
              transform:translateY(-100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer.bp3-position-bottom{
    right:0;
    bottom:0;
    left:0;
    height:50%; }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-enter, .bp3-drawer.bp3-position-bottom.bp3-overlay-appear{
      -webkit-transform:translateY(100%);
              transform:translateY(100%); }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-enter-active, .bp3-drawer.bp3-position-bottom.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-exit-active{
      -webkit-transform:translateY(100%);
              transform:translateY(100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer.bp3-position-left{
    top:0;
    bottom:0;
    left:0;
    width:50%; }
    .bp3-drawer.bp3-position-left.bp3-overlay-enter, .bp3-drawer.bp3-position-left.bp3-overlay-appear{
      -webkit-transform:translateX(-100%);
              transform:translateX(-100%); }
    .bp3-drawer.bp3-position-left.bp3-overlay-enter-active, .bp3-drawer.bp3-position-left.bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer.bp3-position-left.bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer.bp3-position-left.bp3-overlay-exit-active{
      -webkit-transform:translateX(-100%);
              transform:translateX(-100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer.bp3-position-right{
    top:0;
    right:0;
    bottom:0;
    width:50%; }
    .bp3-drawer.bp3-position-right.bp3-overlay-enter, .bp3-drawer.bp3-position-right.bp3-overlay-appear{
      -webkit-transform:translateX(100%);
              transform:translateX(100%); }
    .bp3-drawer.bp3-position-right.bp3-overlay-enter-active, .bp3-drawer.bp3-position-right.bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer.bp3-position-right.bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer.bp3-position-right.bp3-overlay-exit-active{
      -webkit-transform:translateX(100%);
              transform:translateX(100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
  .bp3-position-right):not(.bp3-vertical){
    top:0;
    right:0;
    bottom:0;
    width:50%; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-enter, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-appear{
      -webkit-transform:translateX(100%);
              transform:translateX(100%); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-enter-active, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-exit-active{
      -webkit-transform:translateX(100%);
              transform:translateX(100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
  .bp3-position-right).bp3-vertical{
    right:0;
    bottom:0;
    left:0;
    height:50%; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-enter, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-appear{
      -webkit-transform:translateY(100%);
              transform:translateY(100%); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-enter-active, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-exit-active{
      -webkit-transform:translateY(100%);
              transform:translateY(100%);
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
      -webkit-transition-delay:0;
              transition-delay:0; }
  .bp3-drawer.bp3-dark,
  .bp3-dark .bp3-drawer{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
    background:#30404d;
    color:#f5f8fa; }

.bp3-drawer-header{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  position:relative;
  border-radius:0;
  -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
  min-height:40px;
  padding:5px;
  padding-left:20px; }
  .bp3-drawer-header .bp3-icon-large,
  .bp3-drawer-header .bp3-icon{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    margin-right:10px;
    color:#5c7080; }
  .bp3-drawer-header .bp3-heading{
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    margin:0;
    line-height:inherit; }
    .bp3-drawer-header .bp3-heading:last-child{
      margin-right:20px; }
  .bp3-dark .bp3-drawer-header{
    -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:0 1px 0 rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-drawer-header .bp3-icon-large,
    .bp3-dark .bp3-drawer-header .bp3-icon{
      color:#a7b6c2; }

.bp3-drawer-body{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  overflow:auto;
  line-height:18px; }

.bp3-drawer-footer{
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  position:relative;
  -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
  padding:10px 20px; }
  .bp3-dark .bp3-drawer-footer{
    -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.4); }
.bp3-editable-text{
  display:inline-block;
  position:relative;
  cursor:text;
  max-width:100%;
  vertical-align:top;
  white-space:nowrap; }
  .bp3-editable-text::before{
    position:absolute;
    top:-3px;
    right:-3px;
    bottom:-3px;
    left:-3px;
    border-radius:3px;
    content:"";
    -webkit-transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-editable-text:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-editable-text.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
    background-color:#ffffff; }
  .bp3-editable-text.bp3-disabled::before{
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-editable-text.bp3-intent-primary .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-primary .bp3-editable-text-content{
    color:#137cbd; }
  .bp3-editable-text.bp3-intent-primary:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(19, 124, 189, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(19, 124, 189, 0.4); }
  .bp3-editable-text.bp3-intent-primary.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-success .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-success .bp3-editable-text-content{
    color:#0f9960; }
  .bp3-editable-text.bp3-intent-success:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px rgba(15, 153, 96, 0.4);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px rgba(15, 153, 96, 0.4); }
  .bp3-editable-text.bp3-intent-success.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-warning .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-warning .bp3-editable-text-content{
    color:#d9822b; }
  .bp3-editable-text.bp3-intent-warning:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px rgba(217, 130, 43, 0.4);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px rgba(217, 130, 43, 0.4); }
  .bp3-editable-text.bp3-intent-warning.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-danger .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-danger .bp3-editable-text-content{
    color:#db3737; }
  .bp3-editable-text.bp3-intent-danger:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px rgba(219, 55, 55, 0.4);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px rgba(219, 55, 55, 0.4); }
  .bp3-editable-text.bp3-intent-danger.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-editable-text:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(255, 255, 255, 0.15);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(255, 255, 255, 0.15); }
  .bp3-dark .bp3-editable-text.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background-color:rgba(16, 22, 26, 0.3); }
  .bp3-dark .bp3-editable-text.bp3-disabled::before{
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-dark .bp3-editable-text.bp3-intent-primary .bp3-editable-text-content{
    color:#48aff0; }
  .bp3-dark .bp3-editable-text.bp3-intent-primary:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(72, 175, 240, 0), 0 0 0 0 rgba(72, 175, 240, 0), inset 0 0 0 1px rgba(72, 175, 240, 0.4);
            box-shadow:0 0 0 0 rgba(72, 175, 240, 0), 0 0 0 0 rgba(72, 175, 240, 0), inset 0 0 0 1px rgba(72, 175, 240, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-primary.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #48aff0, 0 0 0 3px rgba(72, 175, 240, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #48aff0, 0 0 0 3px rgba(72, 175, 240, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-success .bp3-editable-text-content{
    color:#3dcc91; }
  .bp3-dark .bp3-editable-text.bp3-intent-success:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(61, 204, 145, 0), 0 0 0 0 rgba(61, 204, 145, 0), inset 0 0 0 1px rgba(61, 204, 145, 0.4);
            box-shadow:0 0 0 0 rgba(61, 204, 145, 0), 0 0 0 0 rgba(61, 204, 145, 0), inset 0 0 0 1px rgba(61, 204, 145, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-success.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #3dcc91, 0 0 0 3px rgba(61, 204, 145, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #3dcc91, 0 0 0 3px rgba(61, 204, 145, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-warning .bp3-editable-text-content{
    color:#ffb366; }
  .bp3-dark .bp3-editable-text.bp3-intent-warning:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(255, 179, 102, 0), 0 0 0 0 rgba(255, 179, 102, 0), inset 0 0 0 1px rgba(255, 179, 102, 0.4);
            box-shadow:0 0 0 0 rgba(255, 179, 102, 0), 0 0 0 0 rgba(255, 179, 102, 0), inset 0 0 0 1px rgba(255, 179, 102, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-warning.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #ffb366, 0 0 0 3px rgba(255, 179, 102, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #ffb366, 0 0 0 3px rgba(255, 179, 102, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-danger .bp3-editable-text-content{
    color:#ff7373; }
  .bp3-dark .bp3-editable-text.bp3-intent-danger:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(255, 115, 115, 0), 0 0 0 0 rgba(255, 115, 115, 0), inset 0 0 0 1px rgba(255, 115, 115, 0.4);
            box-shadow:0 0 0 0 rgba(255, 115, 115, 0), 0 0 0 0 rgba(255, 115, 115, 0), inset 0 0 0 1px rgba(255, 115, 115, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-danger.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #ff7373, 0 0 0 3px rgba(255, 115, 115, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #ff7373, 0 0 0 3px rgba(255, 115, 115, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-editable-text-input,
.bp3-editable-text-content{
  display:inherit;
  position:relative;
  min-width:inherit;
  max-width:inherit;
  vertical-align:top;
  text-transform:inherit;
  letter-spacing:inherit;
  color:inherit;
  font:inherit;
  resize:none; }

.bp3-editable-text-input{
  border:none;
  -webkit-box-shadow:none;
          box-shadow:none;
  background:none;
  width:100%;
  padding:0;
  white-space:pre-wrap; }
  .bp3-editable-text-input::-webkit-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input::-moz-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input:-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input::-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input::placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-editable-text-input:focus{
    outline:none; }
  .bp3-editable-text-input::-ms-clear{
    display:none; }

.bp3-editable-text-content{
  overflow:hidden;
  padding-right:2px;
  text-overflow:ellipsis;
  white-space:pre; }
  .bp3-editable-text-editing > .bp3-editable-text-content{
    position:absolute;
    left:0;
    visibility:hidden; }
  .bp3-editable-text-placeholder > .bp3-editable-text-content{
    color:rgba(92, 112, 128, 0.6); }
    .bp3-dark .bp3-editable-text-placeholder > .bp3-editable-text-content{
      color:rgba(167, 182, 194, 0.6); }

.bp3-editable-text.bp3-multiline{
  display:block; }
  .bp3-editable-text.bp3-multiline .bp3-editable-text-content{
    overflow:auto;
    white-space:pre-wrap;
    word-wrap:break-word; }
.bp3-control-group{
  -webkit-transform:translateZ(0);
          transform:translateZ(0);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:stretch;
      -ms-flex-align:stretch;
          align-items:stretch; }
  .bp3-control-group > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-control-group > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-control-group .bp3-button,
  .bp3-control-group .bp3-html-select,
  .bp3-control-group .bp3-input,
  .bp3-control-group .bp3-select{
    position:relative; }
  .bp3-control-group .bp3-input{
    z-index:2;
    border-radius:inherit; }
    .bp3-control-group .bp3-input:focus{
      z-index:14;
      border-radius:3px; }
    .bp3-control-group .bp3-input[class*="bp3-intent"]{
      z-index:13; }
      .bp3-control-group .bp3-input[class*="bp3-intent"]:focus{
        z-index:15; }
    .bp3-control-group .bp3-input[readonly], .bp3-control-group .bp3-input:disabled, .bp3-control-group .bp3-input.bp3-disabled{
      z-index:1; }
  .bp3-control-group .bp3-input-group[class*="bp3-intent"] .bp3-input{
    z-index:13; }
    .bp3-control-group .bp3-input-group[class*="bp3-intent"] .bp3-input:focus{
      z-index:15; }
  .bp3-control-group .bp3-button,
  .bp3-control-group .bp3-html-select select,
  .bp3-control-group .bp3-select select{
    -webkit-transform:translateZ(0);
            transform:translateZ(0);
    z-index:4;
    border-radius:inherit; }
    .bp3-control-group .bp3-button:focus,
    .bp3-control-group .bp3-html-select select:focus,
    .bp3-control-group .bp3-select select:focus{
      z-index:5; }
    .bp3-control-group .bp3-button:hover,
    .bp3-control-group .bp3-html-select select:hover,
    .bp3-control-group .bp3-select select:hover{
      z-index:6; }
    .bp3-control-group .bp3-button:active,
    .bp3-control-group .bp3-html-select select:active,
    .bp3-control-group .bp3-select select:active{
      z-index:7; }
    .bp3-control-group .bp3-button[readonly], .bp3-control-group .bp3-button:disabled, .bp3-control-group .bp3-button.bp3-disabled,
    .bp3-control-group .bp3-html-select select[readonly],
    .bp3-control-group .bp3-html-select select:disabled,
    .bp3-control-group .bp3-html-select select.bp3-disabled,
    .bp3-control-group .bp3-select select[readonly],
    .bp3-control-group .bp3-select select:disabled,
    .bp3-control-group .bp3-select select.bp3-disabled{
      z-index:3; }
    .bp3-control-group .bp3-button[class*="bp3-intent"],
    .bp3-control-group .bp3-html-select select[class*="bp3-intent"],
    .bp3-control-group .bp3-select select[class*="bp3-intent"]{
      z-index:9; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:focus,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:focus,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:focus{
        z-index:10; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:hover,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:hover,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:hover{
        z-index:11; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:active,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:active,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:active{
        z-index:12; }
      .bp3-control-group .bp3-button[class*="bp3-intent"][readonly], .bp3-control-group .bp3-button[class*="bp3-intent"]:disabled, .bp3-control-group .bp3-button[class*="bp3-intent"].bp3-disabled,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"][readonly],
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:disabled,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"].bp3-disabled,
      .bp3-control-group .bp3-select select[class*="bp3-intent"][readonly],
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:disabled,
      .bp3-control-group .bp3-select select[class*="bp3-intent"].bp3-disabled{
        z-index:8; }
  .bp3-control-group .bp3-input-group > .bp3-icon,
  .bp3-control-group .bp3-input-group > .bp3-button,
  .bp3-control-group .bp3-input-group > .bp3-input-action{
    z-index:16; }
  .bp3-control-group .bp3-select::after,
  .bp3-control-group .bp3-html-select::after,
  .bp3-control-group .bp3-select > .bp3-icon,
  .bp3-control-group .bp3-html-select > .bp3-icon{
    z-index:17; }
  .bp3-control-group:not(.bp3-vertical) > *{
    margin-right:-1px; }
  .bp3-dark .bp3-control-group:not(.bp3-vertical) > *{
    margin-right:0; }
  .bp3-dark .bp3-control-group:not(.bp3-vertical) > .bp3-button + .bp3-button{
    margin-left:1px; }
  .bp3-control-group .bp3-popover-wrapper,
  .bp3-control-group .bp3-popover-target{
    border-radius:inherit; }
  .bp3-control-group > :first-child{
    border-radius:3px 0 0 3px; }
  .bp3-control-group > :last-child{
    margin-right:0;
    border-radius:0 3px 3px 0; }
  .bp3-control-group > :only-child{
    margin-right:0;
    border-radius:3px; }
  .bp3-control-group .bp3-input-group .bp3-button{
    border-radius:3px; }
  .bp3-control-group > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-control-group.bp3-fill > *:not(.bp3-fixed){
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-control-group.bp3-vertical{
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column; }
    .bp3-control-group.bp3-vertical > *{
      margin-top:-1px; }
    .bp3-control-group.bp3-vertical > :first-child{
      margin-top:0;
      border-radius:3px 3px 0 0; }
    .bp3-control-group.bp3-vertical > :last-child{
      border-radius:0 0 3px 3px; }
.bp3-control{
  display:block;
  position:relative;
  margin-bottom:10px;
  cursor:pointer;
  text-transform:none; }
  .bp3-control input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
  .bp3-control:hover input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#106ba3; }
  .bp3-control input:not(:disabled):active:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background:#0e5a8a; }
  .bp3-control input:disabled:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(19, 124, 189, 0.5); }
  .bp3-dark .bp3-control input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control:hover input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#106ba3; }
  .bp3-dark .bp3-control input:not(:disabled):active:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#0e5a8a; }
  .bp3-dark .bp3-control input:disabled:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(14, 90, 138, 0.5); }
  .bp3-control:not(.bp3-align-right){
    padding-left:26px; }
    .bp3-control:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-26px; }
  .bp3-control.bp3-align-right{
    padding-right:26px; }
    .bp3-control.bp3-align-right .bp3-control-indicator{
      margin-right:-26px; }
  .bp3-control.bp3-disabled{
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-control.bp3-inline{
    display:inline-block;
    margin-right:20px; }
  .bp3-control input{
    position:absolute;
    top:0;
    left:0;
    opacity:0;
    z-index:-1; }
  .bp3-control .bp3-control-indicator{
    display:inline-block;
    position:relative;
    margin-top:-3px;
    margin-right:10px;
    border:none;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    cursor:pointer;
    width:1em;
    height:1em;
    vertical-align:middle;
    font-size:16px;
    -webkit-user-select:none;
       -moz-user-select:none;
        -ms-user-select:none;
            user-select:none; }
    .bp3-control .bp3-control-indicator::before{
      display:block;
      width:1em;
      height:1em;
      content:""; }
  .bp3-control:hover .bp3-control-indicator{
    background-color:#ebf1f5; }
  .bp3-control input:not(:disabled):active ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background:#d8e1e8; }
  .bp3-control input:disabled ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(206, 217, 224, 0.5);
    cursor:not-allowed; }
  .bp3-control input:focus ~ .bp3-control-indicator{
    outline:rgba(19, 124, 189, 0.6) auto 2px;
    outline-offset:2px;
    -moz-outline-radius:6px; }
  .bp3-control.bp3-align-right .bp3-control-indicator{
    float:right;
    margin-top:1px;
    margin-left:10px; }
  .bp3-control.bp3-large{
    font-size:16px; }
    .bp3-control.bp3-large:not(.bp3-align-right){
      padding-left:30px; }
      .bp3-control.bp3-large:not(.bp3-align-right) .bp3-control-indicator{
        margin-left:-30px; }
    .bp3-control.bp3-large.bp3-align-right{
      padding-right:30px; }
      .bp3-control.bp3-large.bp3-align-right .bp3-control-indicator{
        margin-right:-30px; }
    .bp3-control.bp3-large .bp3-control-indicator{
      font-size:20px; }
    .bp3-control.bp3-large.bp3-align-right .bp3-control-indicator{
      margin-top:0; }
  .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    color:#ffffff; }
  .bp3-control.bp3-checkbox:hover input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    background-color:#106ba3; }
  .bp3-control.bp3-checkbox input:not(:disabled):active:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background:#0e5a8a; }
  .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(19, 124, 189, 0.5); }
  .bp3-dark .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-checkbox:hover input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#106ba3; }
  .bp3-dark .bp3-control.bp3-checkbox input:not(:disabled):active:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#0e5a8a; }
  .bp3-dark .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(14, 90, 138, 0.5); }
  .bp3-control.bp3-checkbox .bp3-control-indicator{
    border-radius:3px; }
  .bp3-control.bp3-checkbox input:checked ~ .bp3-control-indicator::before{
    background-image:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M12 5c-.28 0-.53.11-.71.29L7 9.59l-2.29-2.3a1.003 1.003 0 0 0-1.42 1.42l3 3c.18.18.43.29.71.29s.53-.11.71-.29l5-5A1.003 1.003 0 0 0 12 5z' fill='white'/%3e%3c/svg%3e"); }
  .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator::before{
    background-image:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M11 7H5c-.55 0-1 .45-1 1s.45 1 1 1h6c.55 0 1-.45 1-1s-.45-1-1-1z' fill='white'/%3e%3c/svg%3e"); }
  .bp3-control.bp3-radio .bp3-control-indicator{
    border-radius:50%; }
  .bp3-control.bp3-radio input:checked ~ .bp3-control-indicator::before{
    background-image:radial-gradient(#ffffff, #ffffff 28%, transparent 32%); }
  .bp3-control.bp3-radio input:checked:disabled ~ .bp3-control-indicator::before{
    opacity:0.5; }
  .bp3-control.bp3-radio input:focus ~ .bp3-control-indicator{
    -moz-outline-radius:16px; }
  .bp3-control.bp3-switch input ~ .bp3-control-indicator{
    background:rgba(167, 182, 194, 0.5); }
  .bp3-control.bp3-switch:hover input ~ .bp3-control-indicator{
    background:rgba(115, 134, 148, 0.5); }
  .bp3-control.bp3-switch input:not(:disabled):active ~ .bp3-control-indicator{
    background:rgba(92, 112, 128, 0.5); }
  .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator{
    background:rgba(206, 217, 224, 0.5); }
    .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator::before{
      background:rgba(255, 255, 255, 0.8); }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator{
    background:#137cbd; }
  .bp3-control.bp3-switch:hover input:checked ~ .bp3-control-indicator{
    background:#106ba3; }
  .bp3-control.bp3-switch input:checked:not(:disabled):active ~ .bp3-control-indicator{
    background:#0e5a8a; }
  .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator{
    background:rgba(19, 124, 189, 0.5); }
    .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator::before{
      background:rgba(255, 255, 255, 0.8); }
  .bp3-control.bp3-switch:not(.bp3-align-right){
    padding-left:38px; }
    .bp3-control.bp3-switch:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-38px; }
  .bp3-control.bp3-switch.bp3-align-right{
    padding-right:38px; }
    .bp3-control.bp3-switch.bp3-align-right .bp3-control-indicator{
      margin-right:-38px; }
  .bp3-control.bp3-switch .bp3-control-indicator{
    border:none;
    border-radius:1.75em;
    -webkit-box-shadow:none !important;
            box-shadow:none !important;
    width:auto;
    min-width:1.75em;
    -webkit-transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-control.bp3-switch .bp3-control-indicator::before{
      position:absolute;
      left:0;
      margin:2px;
      border-radius:50%;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
      background:#ffffff;
      width:calc(1em - 4px);
      height:calc(1em - 4px);
      -webkit-transition:left 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
      transition:left 100ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator::before{
    left:calc(100% - 1em); }
  .bp3-control.bp3-switch.bp3-large:not(.bp3-align-right){
    padding-left:45px; }
    .bp3-control.bp3-switch.bp3-large:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-45px; }
  .bp3-control.bp3-switch.bp3-large.bp3-align-right{
    padding-right:45px; }
    .bp3-control.bp3-switch.bp3-large.bp3-align-right .bp3-control-indicator{
      margin-right:-45px; }
  .bp3-dark .bp3-control.bp3-switch input ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.5); }
  .bp3-dark .bp3-control.bp3-switch:hover input ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.7); }
  .bp3-dark .bp3-control.bp3-switch input:not(:disabled):active ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.9); }
  .bp3-dark .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator{
    background:rgba(57, 75, 89, 0.5); }
    .bp3-dark .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator::before{
      background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator{
    background:#137cbd; }
  .bp3-dark .bp3-control.bp3-switch:hover input:checked ~ .bp3-control-indicator{
    background:#106ba3; }
  .bp3-dark .bp3-control.bp3-switch input:checked:not(:disabled):active ~ .bp3-control-indicator{
    background:#0e5a8a; }
  .bp3-dark .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator{
    background:rgba(14, 90, 138, 0.5); }
    .bp3-dark .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator::before{
      background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-switch .bp3-control-indicator::before{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background:#394b59; }
  .bp3-dark .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator::before{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-control.bp3-switch .bp3-switch-inner-text{
    text-align:center;
    font-size:0.7em; }
  .bp3-control.bp3-switch .bp3-control-indicator-child:first-child{
    visibility:hidden;
    margin-right:1.2em;
    margin-left:0.5em;
    line-height:0; }
  .bp3-control.bp3-switch .bp3-control-indicator-child:last-child{
    visibility:visible;
    margin-right:0.5em;
    margin-left:1.2em;
    line-height:1em; }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator .bp3-control-indicator-child:first-child{
    visibility:visible;
    line-height:1em; }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator .bp3-control-indicator-child:last-child{
    visibility:hidden;
    line-height:0; }
  .bp3-dark .bp3-control{
    color:#f5f8fa; }
    .bp3-dark .bp3-control.bp3-disabled{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-control .bp3-control-indicator{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#394b59;
      background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
      background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0)); }
    .bp3-dark .bp3-control:hover .bp3-control-indicator{
      background-color:#30404d; }
    .bp3-dark .bp3-control input:not(:disabled):active ~ .bp3-control-indicator{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background:#202b33; }
    .bp3-dark .bp3-control input:disabled ~ .bp3-control-indicator{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(57, 75, 89, 0.5);
      cursor:not-allowed; }
    .bp3-dark .bp3-control.bp3-checkbox input:disabled:checked ~ .bp3-control-indicator, .bp3-dark .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
      color:rgba(167, 182, 194, 0.6); }
.bp3-file-input{
  display:inline-block;
  position:relative;
  cursor:pointer;
  height:30px; }
  .bp3-file-input input{
    opacity:0;
    margin:0;
    min-width:200px; }
    .bp3-file-input input:disabled + .bp3-file-upload-input,
    .bp3-file-input input.bp3-disabled + .bp3-file-upload-input{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(206, 217, 224, 0.5);
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6);
      resize:none; }
      .bp3-file-input input:disabled + .bp3-file-upload-input::after,
      .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after{
        outline:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        background-color:rgba(206, 217, 224, 0.5);
        background-image:none;
        cursor:not-allowed;
        color:rgba(92, 112, 128, 0.6); }
        .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active, .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active:hover,
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active,
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active:hover{
          background:rgba(206, 217, 224, 0.7); }
      .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input, .bp3-dark
      .bp3-file-input input.bp3-disabled + .bp3-file-upload-input{
        -webkit-box-shadow:none;
                box-shadow:none;
        background:rgba(57, 75, 89, 0.5);
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input::after, .bp3-dark
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after{
          -webkit-box-shadow:none;
                  box-shadow:none;
          background-color:rgba(57, 75, 89, 0.5);
          background-image:none;
          color:rgba(167, 182, 194, 0.6); }
          .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active, .bp3-dark
          .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active{
            background:rgba(57, 75, 89, 0.7); }
  .bp3-file-input.bp3-file-input-has-selection .bp3-file-upload-input{
    color:#182026; }
  .bp3-dark .bp3-file-input.bp3-file-input-has-selection .bp3-file-upload-input{
    color:#f5f8fa; }
  .bp3-file-input.bp3-fill{
    width:100%; }
  .bp3-file-input.bp3-large,
  .bp3-large .bp3-file-input{
    height:40px; }
  .bp3-file-input .bp3-file-upload-input-custom-text::after{
    content:attr(bp3-button-text); }

.bp3-file-upload-input{
  outline:none;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
  background:#ffffff;
  height:30px;
  padding:0 10px;
  vertical-align:middle;
  line-height:30px;
  color:#182026;
  font-size:14px;
  font-weight:400;
  -webkit-transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  -webkit-appearance:none;
     -moz-appearance:none;
          appearance:none;
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  position:absolute;
  top:0;
  right:0;
  left:0;
  padding-right:80px;
  color:rgba(92, 112, 128, 0.6);
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-file-upload-input::-webkit-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input::-moz-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input:-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input::-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input::placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-file-upload-input:focus, .bp3-file-upload-input.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-file-upload-input[type="search"], .bp3-file-upload-input.bp3-round{
    border-radius:30px;
    -webkit-box-sizing:border-box;
            box-sizing:border-box;
    padding-left:10px; }
  .bp3-file-upload-input[readonly]{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-file-upload-input:disabled, .bp3-file-upload-input.bp3-disabled{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(206, 217, 224, 0.5);
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6);
    resize:none; }
  .bp3-file-upload-input::after{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    color:#182026;
    min-width:24px;
    min-height:24px;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    position:absolute;
    top:0;
    right:0;
    margin:3px;
    border-radius:3px;
    width:70px;
    text-align:center;
    line-height:24px;
    content:"Browse"; }
    .bp3-file-upload-input::after:hover{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
      background-clip:padding-box;
      background-color:#ebf1f5; }
    .bp3-file-upload-input::after:active, .bp3-file-upload-input::after.bp3-active{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#d8e1e8;
      background-image:none; }
    .bp3-file-upload-input::after:disabled, .bp3-file-upload-input::after.bp3-disabled{
      outline:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(206, 217, 224, 0.5);
      background-image:none;
      cursor:not-allowed;
      color:rgba(92, 112, 128, 0.6); }
      .bp3-file-upload-input::after:disabled.bp3-active, .bp3-file-upload-input::after:disabled.bp3-active:hover, .bp3-file-upload-input::after.bp3-disabled.bp3-active, .bp3-file-upload-input::after.bp3-disabled.bp3-active:hover{
        background:rgba(206, 217, 224, 0.7); }
  .bp3-file-upload-input:hover::after{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#ebf1f5; }
  .bp3-file-upload-input:active::after{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#d8e1e8;
    background-image:none; }
  .bp3-large .bp3-file-upload-input{
    height:40px;
    line-height:40px;
    font-size:16px;
    padding-right:95px; }
    .bp3-large .bp3-file-upload-input[type="search"], .bp3-large .bp3-file-upload-input.bp3-round{
      padding:0 15px; }
    .bp3-large .bp3-file-upload-input::after{
      min-width:30px;
      min-height:30px;
      margin:5px;
      width:85px;
      line-height:30px; }
  .bp3-dark .bp3-file-upload-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#f5f8fa;
    color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-file-upload-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-file-upload-input:disabled, .bp3-dark .bp3-file-upload-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(57, 75, 89, 0.5);
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::after{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#394b59;
      background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
      background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
      color:#f5f8fa; }
      .bp3-dark .bp3-file-upload-input::after:hover, .bp3-dark .bp3-file-upload-input::after:active, .bp3-dark .bp3-file-upload-input::after.bp3-active{
        color:#f5f8fa; }
      .bp3-dark .bp3-file-upload-input::after:hover{
        -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
        background-color:#30404d; }
      .bp3-dark .bp3-file-upload-input::after:active, .bp3-dark .bp3-file-upload-input::after.bp3-active{
        -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
                box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
        background-color:#202b33;
        background-image:none; }
      .bp3-dark .bp3-file-upload-input::after:disabled, .bp3-dark .bp3-file-upload-input::after.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none;
        background-color:rgba(57, 75, 89, 0.5);
        background-image:none;
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-file-upload-input::after:disabled.bp3-active, .bp3-dark .bp3-file-upload-input::after.bp3-disabled.bp3-active{
          background:rgba(57, 75, 89, 0.7); }
      .bp3-dark .bp3-file-upload-input::after .bp3-button-spinner .bp3-spinner-head{
        background:rgba(16, 22, 26, 0.5);
        stroke:#8a9ba8; }
    .bp3-dark .bp3-file-upload-input:hover::after{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#30404d; }
    .bp3-dark .bp3-file-upload-input:active::after{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#202b33;
      background-image:none; }

.bp3-file-upload-input::after{
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1); }
.bp3-form-group{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:0 0 15px; }
  .bp3-form-group label.bp3-label{
    margin-bottom:5px; }
  .bp3-form-group .bp3-control{
    margin-top:7px; }
  .bp3-form-group .bp3-form-helper-text{
    margin-top:5px;
    color:#5c7080;
    font-size:12px; }
  .bp3-form-group.bp3-intent-primary .bp3-form-helper-text{
    color:#106ba3; }
  .bp3-form-group.bp3-intent-success .bp3-form-helper-text{
    color:#0d8050; }
  .bp3-form-group.bp3-intent-warning .bp3-form-helper-text{
    color:#bf7326; }
  .bp3-form-group.bp3-intent-danger .bp3-form-helper-text{
    color:#c23030; }
  .bp3-form-group.bp3-inline{
    -webkit-box-orient:horizontal;
    -webkit-box-direction:normal;
        -ms-flex-direction:row;
            flex-direction:row;
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start; }
    .bp3-form-group.bp3-inline.bp3-large label.bp3-label{
      margin:0 10px 0 0;
      line-height:40px; }
    .bp3-form-group.bp3-inline label.bp3-label{
      margin:0 10px 0 0;
      line-height:30px; }
  .bp3-form-group.bp3-disabled .bp3-label,
  .bp3-form-group.bp3-disabled .bp3-text-muted,
  .bp3-form-group.bp3-disabled .bp3-form-helper-text{
    color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-dark .bp3-form-group.bp3-intent-primary .bp3-form-helper-text{
    color:#48aff0; }
  .bp3-dark .bp3-form-group.bp3-intent-success .bp3-form-helper-text{
    color:#3dcc91; }
  .bp3-dark .bp3-form-group.bp3-intent-warning .bp3-form-helper-text{
    color:#ffb366; }
  .bp3-dark .bp3-form-group.bp3-intent-danger .bp3-form-helper-text{
    color:#ff7373; }
  .bp3-dark .bp3-form-group .bp3-form-helper-text{
    color:#a7b6c2; }
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-label,
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-text-muted,
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-form-helper-text{
    color:rgba(167, 182, 194, 0.6) !important; }
.bp3-input-group{
  display:block;
  position:relative; }
  .bp3-input-group .bp3-input{
    position:relative;
    width:100%; }
    .bp3-input-group .bp3-input:not(:first-child){
      padding-left:30px; }
    .bp3-input-group .bp3-input:not(:last-child){
      padding-right:30px; }
  .bp3-input-group .bp3-input-action,
  .bp3-input-group > .bp3-button,
  .bp3-input-group > .bp3-icon{
    position:absolute;
    top:0; }
    .bp3-input-group .bp3-input-action:first-child,
    .bp3-input-group > .bp3-button:first-child,
    .bp3-input-group > .bp3-icon:first-child{
      left:0; }
    .bp3-input-group .bp3-input-action:last-child,
    .bp3-input-group > .bp3-button:last-child,
    .bp3-input-group > .bp3-icon:last-child{
      right:0; }
  .bp3-input-group .bp3-button{
    min-width:24px;
    min-height:24px;
    margin:3px;
    padding:0 7px; }
    .bp3-input-group .bp3-button:empty{
      padding:0; }
  .bp3-input-group > .bp3-icon{
    z-index:1;
    color:#5c7080; }
    .bp3-input-group > .bp3-icon:empty{
      line-height:1;
      font-family:"Icons16", sans-serif;
      font-size:16px;
      font-weight:400;
      font-style:normal;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased; }
  .bp3-input-group > .bp3-icon,
  .bp3-input-group .bp3-input-action > .bp3-spinner{
    margin:7px; }
  .bp3-input-group .bp3-tag{
    margin:5px; }
  .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus),
  .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus){
    color:#5c7080; }
    .bp3-dark .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus), .bp3-dark
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus){
      color:#a7b6c2; }
    .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-standard, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-large,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-standard,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-large{
      color:#5c7080; }
  .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled,
  .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled{
    color:rgba(92, 112, 128, 0.6) !important; }
    .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon-standard, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon-large,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon-standard,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon-large{
      color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-input-group.bp3-disabled{
    cursor:not-allowed; }
    .bp3-input-group.bp3-disabled .bp3-icon{
      color:rgba(92, 112, 128, 0.6); }
  .bp3-input-group.bp3-large .bp3-button{
    min-width:30px;
    min-height:30px;
    margin:5px; }
  .bp3-input-group.bp3-large > .bp3-icon,
  .bp3-input-group.bp3-large .bp3-input-action > .bp3-spinner{
    margin:12px; }
  .bp3-input-group.bp3-large .bp3-input{
    height:40px;
    line-height:40px;
    font-size:16px; }
    .bp3-input-group.bp3-large .bp3-input[type="search"], .bp3-input-group.bp3-large .bp3-input.bp3-round{
      padding:0 15px; }
    .bp3-input-group.bp3-large .bp3-input:not(:first-child){
      padding-left:40px; }
    .bp3-input-group.bp3-large .bp3-input:not(:last-child){
      padding-right:40px; }
  .bp3-input-group.bp3-small .bp3-button{
    min-width:20px;
    min-height:20px;
    margin:2px; }
  .bp3-input-group.bp3-small .bp3-tag{
    min-width:20px;
    min-height:20px;
    margin:2px; }
  .bp3-input-group.bp3-small > .bp3-icon,
  .bp3-input-group.bp3-small .bp3-input-action > .bp3-spinner{
    margin:4px; }
  .bp3-input-group.bp3-small .bp3-input{
    height:24px;
    padding-right:8px;
    padding-left:8px;
    line-height:24px;
    font-size:12px; }
    .bp3-input-group.bp3-small .bp3-input[type="search"], .bp3-input-group.bp3-small .bp3-input.bp3-round{
      padding:0 12px; }
    .bp3-input-group.bp3-small .bp3-input:not(:first-child){
      padding-left:24px; }
    .bp3-input-group.bp3-small .bp3-input:not(:last-child){
      padding-right:24px; }
  .bp3-input-group.bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    width:100%; }
  .bp3-input-group.bp3-round .bp3-button,
  .bp3-input-group.bp3-round .bp3-input,
  .bp3-input-group.bp3-round .bp3-tag{
    border-radius:30px; }
  .bp3-dark .bp3-input-group .bp3-icon{
    color:#a7b6c2; }
  .bp3-dark .bp3-input-group.bp3-disabled .bp3-icon{
    color:rgba(167, 182, 194, 0.6); }
  .bp3-input-group.bp3-intent-primary .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-primary .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-primary .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #137cbd;
              box-shadow:inset 0 0 0 1px #137cbd; }
    .bp3-input-group.bp3-intent-primary .bp3-input:disabled, .bp3-input-group.bp3-intent-primary .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-primary > .bp3-icon{
    color:#106ba3; }
    .bp3-dark .bp3-input-group.bp3-intent-primary > .bp3-icon{
      color:#48aff0; }
  .bp3-input-group.bp3-intent-success .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-success .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-success .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #0f9960;
              box-shadow:inset 0 0 0 1px #0f9960; }
    .bp3-input-group.bp3-intent-success .bp3-input:disabled, .bp3-input-group.bp3-intent-success .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-success > .bp3-icon{
    color:#0d8050; }
    .bp3-dark .bp3-input-group.bp3-intent-success > .bp3-icon{
      color:#3dcc91; }
  .bp3-input-group.bp3-intent-warning .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-warning .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-warning .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #d9822b;
              box-shadow:inset 0 0 0 1px #d9822b; }
    .bp3-input-group.bp3-intent-warning .bp3-input:disabled, .bp3-input-group.bp3-intent-warning .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-warning > .bp3-icon{
    color:#bf7326; }
    .bp3-dark .bp3-input-group.bp3-intent-warning > .bp3-icon{
      color:#ffb366; }
  .bp3-input-group.bp3-intent-danger .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-danger .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-danger .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #db3737;
              box-shadow:inset 0 0 0 1px #db3737; }
    .bp3-input-group.bp3-intent-danger .bp3-input:disabled, .bp3-input-group.bp3-intent-danger .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-danger > .bp3-icon{
    color:#c23030; }
    .bp3-dark .bp3-input-group.bp3-intent-danger > .bp3-icon{
      color:#ff7373; }
.bp3-input{
  outline:none;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
  background:#ffffff;
  height:30px;
  padding:0 10px;
  vertical-align:middle;
  line-height:30px;
  color:#182026;
  font-size:14px;
  font-weight:400;
  -webkit-transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  -webkit-appearance:none;
     -moz-appearance:none;
          appearance:none; }
  .bp3-input::-webkit-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input::-moz-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input:-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input::-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input::placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input:focus, .bp3-input.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-input[type="search"], .bp3-input.bp3-round{
    border-radius:30px;
    -webkit-box-sizing:border-box;
            box-sizing:border-box;
    padding-left:10px; }
  .bp3-input[readonly]{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-input:disabled, .bp3-input.bp3-disabled{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(206, 217, 224, 0.5);
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6);
    resize:none; }
  .bp3-input.bp3-large{
    height:40px;
    line-height:40px;
    font-size:16px; }
    .bp3-input.bp3-large[type="search"], .bp3-input.bp3-large.bp3-round{
      padding:0 15px; }
  .bp3-input.bp3-small{
    height:24px;
    padding-right:8px;
    padding-left:8px;
    line-height:24px;
    font-size:12px; }
    .bp3-input.bp3-small[type="search"], .bp3-input.bp3-small.bp3-round{
      padding:0 12px; }
  .bp3-input.bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    width:100%; }
  .bp3-dark .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#f5f8fa; }
    .bp3-dark .bp3-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-input:disabled, .bp3-dark .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(57, 75, 89, 0.5);
      color:rgba(167, 182, 194, 0.6); }
  .bp3-input.bp3-intent-primary{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-primary:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-primary[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #137cbd;
              box-shadow:inset 0 0 0 1px #137cbd; }
    .bp3-input.bp3-intent-primary:disabled, .bp3-input.bp3-intent-primary.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-primary:focus{
        -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-primary[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #137cbd;
                box-shadow:inset 0 0 0 1px #137cbd; }
      .bp3-dark .bp3-input.bp3-intent-primary:disabled, .bp3-dark .bp3-input.bp3-intent-primary.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-success{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-success:focus{
      -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-success[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #0f9960;
              box-shadow:inset 0 0 0 1px #0f9960; }
    .bp3-input.bp3-intent-success:disabled, .bp3-input.bp3-intent-success.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-success{
      -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-success:focus{
        -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #0f9960, 0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-success[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #0f9960;
                box-shadow:inset 0 0 0 1px #0f9960; }
      .bp3-dark .bp3-input.bp3-intent-success:disabled, .bp3-dark .bp3-input.bp3-intent-success.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-warning{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-warning:focus{
      -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-warning[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #d9822b;
              box-shadow:inset 0 0 0 1px #d9822b; }
    .bp3-input.bp3-intent-warning:disabled, .bp3-input.bp3-intent-warning.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-warning:focus{
        -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #d9822b, 0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-warning[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #d9822b;
                box-shadow:inset 0 0 0 1px #d9822b; }
      .bp3-dark .bp3-input.bp3-intent-warning:disabled, .bp3-dark .bp3-input.bp3-intent-warning.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-danger{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-danger:focus{
      -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-danger[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #db3737;
              box-shadow:inset 0 0 0 1px #db3737; }
    .bp3-input.bp3-intent-danger:disabled, .bp3-input.bp3-intent-danger.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-danger:focus{
        -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #db3737, 0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-danger[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #db3737;
                box-shadow:inset 0 0 0 1px #db3737; }
      .bp3-dark .bp3-input.bp3-intent-danger:disabled, .bp3-dark .bp3-input.bp3-intent-danger.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input::-ms-clear{
    display:none; }
textarea.bp3-input{
  max-width:100%;
  padding:10px; }
  textarea.bp3-input, textarea.bp3-input.bp3-large, textarea.bp3-input.bp3-small{
    height:auto;
    line-height:inherit; }
  textarea.bp3-input.bp3-small{
    padding:8px; }
  .bp3-dark textarea.bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background:rgba(16, 22, 26, 0.3);
    color:#f5f8fa; }
    .bp3-dark textarea.bp3-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark textarea.bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark textarea.bp3-input:disabled, .bp3-dark textarea.bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:rgba(57, 75, 89, 0.5);
      color:rgba(167, 182, 194, 0.6); }
label.bp3-label{
  display:block;
  margin-top:0;
  margin-bottom:15px; }
  label.bp3-label .bp3-html-select,
  label.bp3-label .bp3-input,
  label.bp3-label .bp3-select,
  label.bp3-label .bp3-slider,
  label.bp3-label .bp3-popover-wrapper{
    display:block;
    margin-top:5px;
    text-transform:none; }
  label.bp3-label .bp3-button-group{
    margin-top:5px; }
  label.bp3-label .bp3-select select,
  label.bp3-label .bp3-html-select select{
    width:100%;
    vertical-align:top;
    font-weight:400; }
  label.bp3-label.bp3-disabled,
  label.bp3-label.bp3-disabled .bp3-text-muted{
    color:rgba(92, 112, 128, 0.6); }
  label.bp3-label.bp3-inline{
    line-height:30px; }
    label.bp3-label.bp3-inline .bp3-html-select,
    label.bp3-label.bp3-inline .bp3-input,
    label.bp3-label.bp3-inline .bp3-input-group,
    label.bp3-label.bp3-inline .bp3-select,
    label.bp3-label.bp3-inline .bp3-popover-wrapper{
      display:inline-block;
      margin:0 0 0 5px;
      vertical-align:top; }
    label.bp3-label.bp3-inline .bp3-button-group{
      margin:0 0 0 5px; }
    label.bp3-label.bp3-inline .bp3-input-group .bp3-input{
      margin-left:0; }
    label.bp3-label.bp3-inline.bp3-large{
      line-height:40px; }
  label.bp3-label:not(.bp3-inline) .bp3-popover-target{
    display:block; }
  .bp3-dark label.bp3-label{
    color:#f5f8fa; }
    .bp3-dark label.bp3-label.bp3-disabled,
    .bp3-dark label.bp3-label.bp3-disabled .bp3-text-muted{
      color:rgba(167, 182, 194, 0.6); }
.bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button{
  -webkit-box-flex:1;
      -ms-flex:1 1 14px;
          flex:1 1 14px;
  width:30px;
  min-height:0;
  padding:0; }
  .bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button:first-child{
    border-radius:0 3px 0 0; }
  .bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button:last-child{
    border-radius:0 0 3px 0; }

.bp3-numeric-input .bp3-button-group.bp3-vertical:first-child > .bp3-button:first-child{
  border-radius:3px 0 0 0; }

.bp3-numeric-input .bp3-button-group.bp3-vertical:first-child > .bp3-button:last-child{
  border-radius:0 0 0 3px; }

.bp3-numeric-input.bp3-large .bp3-button-group.bp3-vertical > .bp3-button{
  width:40px; }

form{
  display:block; }
.bp3-html-select select,
.bp3-select select{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  border:none;
  border-radius:3px;
  cursor:pointer;
  padding:5px 10px;
  vertical-align:middle;
  text-align:left;
  font-size:14px;
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
  background-color:#f5f8fa;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
  color:#182026;
  border-radius:3px;
  width:100%;
  height:30px;
  padding:0 25px 0 10px;
  -moz-appearance:none;
  -webkit-appearance:none; }
  .bp3-html-select select > *, .bp3-select select > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-html-select select > .bp3-fill, .bp3-select select > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-html-select select::before,
  .bp3-select select::before, .bp3-html-select select > *, .bp3-select select > *{
    margin-right:7px; }
  .bp3-html-select select:empty::before,
  .bp3-select select:empty::before,
  .bp3-html-select select > :last-child,
  .bp3-select select > :last-child{
    margin-right:0; }
  .bp3-html-select select:hover,
  .bp3-select select:hover{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#ebf1f5; }
  .bp3-html-select select:active,
  .bp3-select select:active, .bp3-html-select select.bp3-active,
  .bp3-select select.bp3-active{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#d8e1e8;
    background-image:none; }
  .bp3-html-select select:disabled,
  .bp3-select select:disabled, .bp3-html-select select.bp3-disabled,
  .bp3-select select.bp3-disabled{
    outline:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    background-color:rgba(206, 217, 224, 0.5);
    background-image:none;
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
    .bp3-html-select select:disabled.bp3-active,
    .bp3-select select:disabled.bp3-active, .bp3-html-select select:disabled.bp3-active:hover,
    .bp3-select select:disabled.bp3-active:hover, .bp3-html-select select.bp3-disabled.bp3-active,
    .bp3-select select.bp3-disabled.bp3-active, .bp3-html-select select.bp3-disabled.bp3-active:hover,
    .bp3-select select.bp3-disabled.bp3-active:hover{
      background:rgba(206, 217, 224, 0.7); }

.bp3-html-select.bp3-minimal select,
.bp3-select.bp3-minimal select{
  -webkit-box-shadow:none;
          box-shadow:none;
  background:none; }
  .bp3-html-select.bp3-minimal select:hover,
  .bp3-select.bp3-minimal select:hover{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(167, 182, 194, 0.3);
    text-decoration:none;
    color:#182026; }
  .bp3-html-select.bp3-minimal select:active,
  .bp3-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal select.bp3-active,
  .bp3-select.bp3-minimal select.bp3-active{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:rgba(115, 134, 148, 0.3);
    color:#182026; }
  .bp3-html-select.bp3-minimal select:disabled,
  .bp3-select.bp3-minimal select:disabled, .bp3-html-select.bp3-minimal select:disabled:hover,
  .bp3-select.bp3-minimal select:disabled:hover, .bp3-html-select.bp3-minimal select.bp3-disabled,
  .bp3-select.bp3-minimal select.bp3-disabled, .bp3-html-select.bp3-minimal select.bp3-disabled:hover,
  .bp3-select.bp3-minimal select.bp3-disabled:hover{
    background:none;
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
    .bp3-html-select.bp3-minimal select:disabled.bp3-active,
    .bp3-select.bp3-minimal select:disabled.bp3-active, .bp3-html-select.bp3-minimal select:disabled:hover.bp3-active,
    .bp3-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-html-select.bp3-minimal select.bp3-disabled.bp3-active,
    .bp3-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-disabled:hover.bp3-active,
    .bp3-select.bp3-minimal select.bp3-disabled:hover.bp3-active{
      background:rgba(115, 134, 148, 0.3); }
  .bp3-dark .bp3-html-select.bp3-minimal select, .bp3-html-select.bp3-minimal .bp3-dark select,
  .bp3-dark .bp3-select.bp3-minimal select, .bp3-select.bp3-minimal .bp3-dark select{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:none;
    color:inherit; }
    .bp3-dark .bp3-html-select.bp3-minimal select:hover, .bp3-html-select.bp3-minimal .bp3-dark select:hover,
    .bp3-dark .bp3-select.bp3-minimal select:hover, .bp3-select.bp3-minimal .bp3-dark select:hover, .bp3-dark .bp3-html-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal .bp3-dark select:active,
    .bp3-dark .bp3-select.bp3-minimal select:active, .bp3-select.bp3-minimal .bp3-dark select:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-active,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none; }
    .bp3-dark .bp3-html-select.bp3-minimal select:hover, .bp3-html-select.bp3-minimal .bp3-dark select:hover,
    .bp3-dark .bp3-select.bp3-minimal select:hover, .bp3-select.bp3-minimal .bp3-dark select:hover{
      background:rgba(138, 155, 168, 0.15); }
    .bp3-dark .bp3-html-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal .bp3-dark select:active,
    .bp3-dark .bp3-select.bp3-minimal select:active, .bp3-select.bp3-minimal .bp3-dark select:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-active,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-active{
      background:rgba(138, 155, 168, 0.3);
      color:#f5f8fa; }
    .bp3-dark .bp3-html-select.bp3-minimal select:disabled, .bp3-html-select.bp3-minimal .bp3-dark select:disabled,
    .bp3-dark .bp3-select.bp3-minimal select:disabled, .bp3-select.bp3-minimal .bp3-dark select:disabled, .bp3-dark .bp3-html-select.bp3-minimal select:disabled:hover, .bp3-html-select.bp3-minimal .bp3-dark select:disabled:hover,
    .bp3-dark .bp3-select.bp3-minimal select:disabled:hover, .bp3-select.bp3-minimal .bp3-dark select:disabled:hover, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled:hover,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled:hover{
      background:none;
      cursor:not-allowed;
      color:rgba(167, 182, 194, 0.6); }
      .bp3-dark .bp3-html-select.bp3-minimal select:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select:disabled.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select:disabled:hover.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-select.bp3-minimal .bp3-dark select:disabled:hover.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled:hover.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled:hover.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled:hover.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled:hover.bp3-active{
        background:rgba(138, 155, 168, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-primary,
  .bp3-select.bp3-minimal select.bp3-intent-primary{
    color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover,
    .bp3-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-html-select.bp3-minimal select.bp3-intent-primary:active,
    .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover,
    .bp3-select.bp3-minimal select.bp3-intent-primary:hover{
      background:rgba(19, 124, 189, 0.15);
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:active,
    .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active{
      background:rgba(19, 124, 189, 0.3);
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled{
      background:none;
      color:rgba(16, 107, 163, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active{
        background:rgba(19, 124, 189, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
      stroke:#106ba3; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary{
      color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.2);
        color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(72, 175, 240, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-success,
  .bp3-select.bp3-minimal select.bp3-intent-success{
    color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:hover,
    .bp3-select.bp3-minimal select.bp3-intent-success:hover, .bp3-html-select.bp3-minimal select.bp3-intent-success:active,
    .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:hover,
    .bp3-select.bp3-minimal select.bp3-intent-success:hover{
      background:rgba(15, 153, 96, 0.15);
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:active,
    .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active{
      background:rgba(15, 153, 96, 0.3);
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled{
      background:none;
      color:rgba(13, 128, 80, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active{
        background:rgba(15, 153, 96, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-success .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
      stroke:#0d8050; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success{
      color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.2);
        color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(61, 204, 145, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-warning,
  .bp3-select.bp3-minimal select.bp3-intent-warning{
    color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover,
    .bp3-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-html-select.bp3-minimal select.bp3-intent-warning:active,
    .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover,
    .bp3-select.bp3-minimal select.bp3-intent-warning:hover{
      background:rgba(217, 130, 43, 0.15);
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:active,
    .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active{
      background:rgba(217, 130, 43, 0.3);
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled{
      background:none;
      color:rgba(191, 115, 38, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active{
        background:rgba(217, 130, 43, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
      stroke:#bf7326; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning{
      color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.2);
        color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(255, 179, 102, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-danger,
  .bp3-select.bp3-minimal select.bp3-intent-danger{
    color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover,
    .bp3-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-html-select.bp3-minimal select.bp3-intent-danger:active,
    .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active{
      -webkit-box-shadow:none;
              box-shadow:none;
      background:none;
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover,
    .bp3-select.bp3-minimal select.bp3-intent-danger:hover{
      background:rgba(219, 55, 55, 0.15);
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:active,
    .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active{
      background:rgba(219, 55, 55, 0.3);
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled{
      background:none;
      color:rgba(194, 48, 48, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active{
        background:rgba(219, 55, 55, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
      stroke:#c23030; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger{
      color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.2);
        color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(255, 115, 115, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }

.bp3-html-select.bp3-large select,
.bp3-select.bp3-large select{
  height:40px;
  padding-right:35px;
  font-size:16px; }

.bp3-dark .bp3-html-select select, .bp3-dark .bp3-select select{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
  background-color:#394b59;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
  color:#f5f8fa; }
  .bp3-dark .bp3-html-select select:hover, .bp3-dark .bp3-select select:hover, .bp3-dark .bp3-html-select select:active, .bp3-dark .bp3-select select:active, .bp3-dark .bp3-html-select select.bp3-active, .bp3-dark .bp3-select select.bp3-active{
    color:#f5f8fa; }
  .bp3-dark .bp3-html-select select:hover, .bp3-dark .bp3-select select:hover{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#30404d; }
  .bp3-dark .bp3-html-select select:active, .bp3-dark .bp3-select select:active, .bp3-dark .bp3-html-select select.bp3-active, .bp3-dark .bp3-select select.bp3-active{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#202b33;
    background-image:none; }
  .bp3-dark .bp3-html-select select:disabled, .bp3-dark .bp3-select select:disabled, .bp3-dark .bp3-html-select select.bp3-disabled, .bp3-dark .bp3-select select.bp3-disabled{
    -webkit-box-shadow:none;
            box-shadow:none;
    background-color:rgba(57, 75, 89, 0.5);
    background-image:none;
    color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-html-select select:disabled.bp3-active, .bp3-dark .bp3-select select:disabled.bp3-active, .bp3-dark .bp3-html-select select.bp3-disabled.bp3-active, .bp3-dark .bp3-select select.bp3-disabled.bp3-active{
      background:rgba(57, 75, 89, 0.7); }
  .bp3-dark .bp3-html-select select .bp3-button-spinner .bp3-spinner-head, .bp3-dark .bp3-select select .bp3-button-spinner .bp3-spinner-head{
    background:rgba(16, 22, 26, 0.5);
    stroke:#8a9ba8; }

.bp3-html-select select:disabled,
.bp3-select select:disabled{
  -webkit-box-shadow:none;
          box-shadow:none;
  background-color:rgba(206, 217, 224, 0.5);
  cursor:not-allowed;
  color:rgba(92, 112, 128, 0.6); }

.bp3-html-select .bp3-icon,
.bp3-select .bp3-icon, .bp3-select::after{
  position:absolute;
  top:7px;
  right:7px;
  color:#5c7080;
  pointer-events:none; }
  .bp3-html-select .bp3-disabled.bp3-icon,
  .bp3-select .bp3-disabled.bp3-icon, .bp3-disabled.bp3-select::after{
    color:rgba(92, 112, 128, 0.6); }
.bp3-html-select,
.bp3-select{
  display:inline-block;
  position:relative;
  vertical-align:middle;
  letter-spacing:normal; }
  .bp3-html-select select::-ms-expand,
  .bp3-select select::-ms-expand{
    display:none; }
  .bp3-html-select .bp3-icon,
  .bp3-select .bp3-icon{
    color:#5c7080; }
    .bp3-html-select .bp3-icon:hover,
    .bp3-select .bp3-icon:hover{
      color:#182026; }
    .bp3-dark .bp3-html-select .bp3-icon, .bp3-dark
    .bp3-select .bp3-icon{
      color:#a7b6c2; }
      .bp3-dark .bp3-html-select .bp3-icon:hover, .bp3-dark
      .bp3-select .bp3-icon:hover{
        color:#f5f8fa; }
  .bp3-html-select.bp3-large::after,
  .bp3-html-select.bp3-large .bp3-icon,
  .bp3-select.bp3-large::after,
  .bp3-select.bp3-large .bp3-icon{
    top:12px;
    right:12px; }
  .bp3-html-select.bp3-fill,
  .bp3-html-select.bp3-fill select,
  .bp3-select.bp3-fill,
  .bp3-select.bp3-fill select{
    width:100%; }
  .bp3-dark .bp3-html-select option, .bp3-dark
  .bp3-select option{
    background-color:#30404d;
    color:#f5f8fa; }
  .bp3-dark .bp3-html-select::after, .bp3-dark
  .bp3-select::after{
    color:#a7b6c2; }

.bp3-select::after{
  line-height:1;
  font-family:"Icons16", sans-serif;
  font-size:16px;
  font-weight:400;
  font-style:normal;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  content:""; }
.bp3-running-text table, table.bp3-html-table{
  border-spacing:0;
  font-size:14px; }
  .bp3-running-text table th, table.bp3-html-table th,
  .bp3-running-text table td,
  table.bp3-html-table td{
    padding:11px;
    vertical-align:top;
    text-align:left; }
  .bp3-running-text table th, table.bp3-html-table th{
    color:#182026;
    font-weight:600; }
  
  .bp3-running-text table td,
  table.bp3-html-table td{
    color:#182026; }
  .bp3-running-text table tbody tr:first-child th, table.bp3-html-table tbody tr:first-child th,
  .bp3-running-text table tbody tr:first-child td,
  table.bp3-html-table tbody tr:first-child td{
    -webkit-box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15); }
  .bp3-dark .bp3-running-text table th, .bp3-running-text .bp3-dark table th, .bp3-dark table.bp3-html-table th{
    color:#f5f8fa; }
  .bp3-dark .bp3-running-text table td, .bp3-running-text .bp3-dark table td, .bp3-dark table.bp3-html-table td{
    color:#f5f8fa; }
  .bp3-dark .bp3-running-text table tbody tr:first-child th, .bp3-running-text .bp3-dark table tbody tr:first-child th, .bp3-dark table.bp3-html-table tbody tr:first-child th,
  .bp3-dark .bp3-running-text table tbody tr:first-child td,
  .bp3-running-text .bp3-dark table tbody tr:first-child td,
  .bp3-dark table.bp3-html-table tbody tr:first-child td{
    -webkit-box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15);
            box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15); }

table.bp3-html-table.bp3-html-table-condensed th,
table.bp3-html-table.bp3-html-table-condensed td, table.bp3-html-table.bp3-small th,
table.bp3-html-table.bp3-small td{
  padding-top:6px;
  padding-bottom:6px; }

table.bp3-html-table.bp3-html-table-striped tbody tr:nth-child(odd) td{
  background:rgba(191, 204, 214, 0.15); }

table.bp3-html-table.bp3-html-table-bordered th:not(:first-child){
  -webkit-box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-html-table-bordered tbody tr td{
  -webkit-box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15); }
  table.bp3-html-table.bp3-html-table-bordered tbody tr td:not(:first-child){
    -webkit-box-shadow:inset 1px 1px 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 1px 1px 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td{
  -webkit-box-shadow:none;
          box-shadow:none; }
  table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td:not(:first-child){
    -webkit-box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-interactive tbody tr:hover td{
  background-color:rgba(191, 204, 214, 0.3);
  cursor:pointer; }

table.bp3-html-table.bp3-interactive tbody tr:active td{
  background-color:rgba(191, 204, 214, 0.4); }

.bp3-dark table.bp3-html-table.bp3-html-table-striped tbody tr:nth-child(odd) td{
  background:rgba(92, 112, 128, 0.15); }

.bp3-dark table.bp3-html-table.bp3-html-table-bordered th:not(:first-child){
  -webkit-box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15);
          box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15); }

.bp3-dark table.bp3-html-table.bp3-html-table-bordered tbody tr td{
  -webkit-box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15);
          box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15); }
  .bp3-dark table.bp3-html-table.bp3-html-table-bordered tbody tr td:not(:first-child){
    -webkit-box-shadow:inset 1px 1px 0 0 rgba(255, 255, 255, 0.15);
            box-shadow:inset 1px 1px 0 0 rgba(255, 255, 255, 0.15); }

.bp3-dark table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td{
  -webkit-box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15);
          box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15); }
  .bp3-dark table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td:first-child{
    -webkit-box-shadow:none;
            box-shadow:none; }

.bp3-dark table.bp3-html-table.bp3-interactive tbody tr:hover td{
  background-color:rgba(92, 112, 128, 0.3);
  cursor:pointer; }

.bp3-dark table.bp3-html-table.bp3-interactive tbody tr:active td{
  background-color:rgba(92, 112, 128, 0.4); }

.bp3-key-combo{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center; }
  .bp3-key-combo > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-key-combo > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-key-combo::before,
  .bp3-key-combo > *{
    margin-right:5px; }
  .bp3-key-combo:empty::before,
  .bp3-key-combo > :last-child{
    margin-right:0; }

.bp3-hotkey-dialog{
  top:40px;
  padding-bottom:0; }
  .bp3-hotkey-dialog .bp3-dialog-body{
    margin:0;
    padding:0; }
  .bp3-hotkey-dialog .bp3-hotkey-label{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1; }

.bp3-hotkey-column{
  margin:auto;
  max-height:80vh;
  overflow-y:auto;
  padding:30px; }
  .bp3-hotkey-column .bp3-heading{
    margin-bottom:20px; }
    .bp3-hotkey-column .bp3-heading:not(:first-child){
      margin-top:40px; }

.bp3-hotkey{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:justify;
      -ms-flex-pack:justify;
          justify-content:space-between;
  margin-right:0;
  margin-left:0; }
  .bp3-hotkey:not(:last-child){
    margin-bottom:10px; }
.bp3-icon{
  display:inline-block;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  vertical-align:text-bottom; }
  .bp3-icon:not(:empty)::before{
    content:"" !important;
    content:unset !important; }
  .bp3-icon > svg{
    display:block; }
    .bp3-icon > svg:not([fill]){
      fill:currentColor; }

.bp3-icon.bp3-intent-primary, .bp3-icon-standard.bp3-intent-primary, .bp3-icon-large.bp3-intent-primary{
  color:#106ba3; }
  .bp3-dark .bp3-icon.bp3-intent-primary, .bp3-dark .bp3-icon-standard.bp3-intent-primary, .bp3-dark .bp3-icon-large.bp3-intent-primary{
    color:#48aff0; }

.bp3-icon.bp3-intent-success, .bp3-icon-standard.bp3-intent-success, .bp3-icon-large.bp3-intent-success{
  color:#0d8050; }
  .bp3-dark .bp3-icon.bp3-intent-success, .bp3-dark .bp3-icon-standard.bp3-intent-success, .bp3-dark .bp3-icon-large.bp3-intent-success{
    color:#3dcc91; }

.bp3-icon.bp3-intent-warning, .bp3-icon-standard.bp3-intent-warning, .bp3-icon-large.bp3-intent-warning{
  color:#bf7326; }
  .bp3-dark .bp3-icon.bp3-intent-warning, .bp3-dark .bp3-icon-standard.bp3-intent-warning, .bp3-dark .bp3-icon-large.bp3-intent-warning{
    color:#ffb366; }

.bp3-icon.bp3-intent-danger, .bp3-icon-standard.bp3-intent-danger, .bp3-icon-large.bp3-intent-danger{
  color:#c23030; }
  .bp3-dark .bp3-icon.bp3-intent-danger, .bp3-dark .bp3-icon-standard.bp3-intent-danger, .bp3-dark .bp3-icon-large.bp3-intent-danger{
    color:#ff7373; }

span.bp3-icon-standard{
  line-height:1;
  font-family:"Icons16", sans-serif;
  font-size:16px;
  font-weight:400;
  font-style:normal;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  display:inline-block; }

span.bp3-icon-large{
  line-height:1;
  font-family:"Icons20", sans-serif;
  font-size:20px;
  font-weight:400;
  font-style:normal;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  display:inline-block; }

span.bp3-icon:empty{
  line-height:1;
  font-family:"Icons20";
  font-size:inherit;
  font-weight:400;
  font-style:normal; }
  span.bp3-icon:empty::before{
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased; }

.bp3-icon-add::before{
  content:""; }

.bp3-icon-add-column-left::before{
  content:""; }

.bp3-icon-add-column-right::before{
  content:""; }

.bp3-icon-add-row-bottom::before{
  content:""; }

.bp3-icon-add-row-top::before{
  content:""; }

.bp3-icon-add-to-artifact::before{
  content:""; }

.bp3-icon-add-to-folder::before{
  content:""; }

.bp3-icon-airplane::before{
  content:""; }

.bp3-icon-align-center::before{
  content:""; }

.bp3-icon-align-justify::before{
  content:""; }

.bp3-icon-align-left::before{
  content:""; }

.bp3-icon-align-right::before{
  content:""; }

.bp3-icon-alignment-bottom::before{
  content:""; }

.bp3-icon-alignment-horizontal-center::before{
  content:""; }

.bp3-icon-alignment-left::before{
  content:""; }

.bp3-icon-alignment-right::before{
  content:""; }

.bp3-icon-alignment-top::before{
  content:""; }

.bp3-icon-alignment-vertical-center::before{
  content:""; }

.bp3-icon-annotation::before{
  content:""; }

.bp3-icon-application::before{
  content:""; }

.bp3-icon-applications::before{
  content:""; }

.bp3-icon-archive::before{
  content:""; }

.bp3-icon-arrow-bottom-left::before{
  content:"↙"; }

.bp3-icon-arrow-bottom-right::before{
  content:"↘"; }

.bp3-icon-arrow-down::before{
  content:"↓"; }

.bp3-icon-arrow-left::before{
  content:"←"; }

.bp3-icon-arrow-right::before{
  content:"→"; }

.bp3-icon-arrow-top-left::before{
  content:"↖"; }

.bp3-icon-arrow-top-right::before{
  content:"↗"; }

.bp3-icon-arrow-up::before{
  content:"↑"; }

.bp3-icon-arrows-horizontal::before{
  content:"↔"; }

.bp3-icon-arrows-vertical::before{
  content:"↕"; }

.bp3-icon-asterisk::before{
  content:"*"; }

.bp3-icon-automatic-updates::before{
  content:""; }

.bp3-icon-badge::before{
  content:""; }

.bp3-icon-ban-circle::before{
  content:""; }

.bp3-icon-bank-account::before{
  content:""; }

.bp3-icon-barcode::before{
  content:""; }

.bp3-icon-blank::before{
  content:""; }

.bp3-icon-blocked-person::before{
  content:""; }

.bp3-icon-bold::before{
  content:""; }

.bp3-icon-book::before{
  content:""; }

.bp3-icon-bookmark::before{
  content:""; }

.bp3-icon-box::before{
  content:""; }

.bp3-icon-briefcase::before{
  content:""; }

.bp3-icon-bring-data::before{
  content:""; }

.bp3-icon-build::before{
  content:""; }

.bp3-icon-calculator::before{
  content:""; }

.bp3-icon-calendar::before{
  content:""; }

.bp3-icon-camera::before{
  content:""; }

.bp3-icon-caret-down::before{
  content:"⌄"; }

.bp3-icon-caret-left::before{
  content:"〈"; }

.bp3-icon-caret-right::before{
  content:"〉"; }

.bp3-icon-caret-up::before{
  content:"⌃"; }

.bp3-icon-cell-tower::before{
  content:""; }

.bp3-icon-changes::before{
  content:""; }

.bp3-icon-chart::before{
  content:""; }

.bp3-icon-chat::before{
  content:""; }

.bp3-icon-chevron-backward::before{
  content:""; }

.bp3-icon-chevron-down::before{
  content:""; }

.bp3-icon-chevron-forward::before{
  content:""; }

.bp3-icon-chevron-left::before{
  content:""; }

.bp3-icon-chevron-right::before{
  content:""; }

.bp3-icon-chevron-up::before{
  content:""; }

.bp3-icon-circle::before{
  content:""; }

.bp3-icon-circle-arrow-down::before{
  content:""; }

.bp3-icon-circle-arrow-left::before{
  content:""; }

.bp3-icon-circle-arrow-right::before{
  content:""; }

.bp3-icon-circle-arrow-up::before{
  content:""; }

.bp3-icon-citation::before{
  content:""; }

.bp3-icon-clean::before{
  content:""; }

.bp3-icon-clipboard::before{
  content:""; }

.bp3-icon-cloud::before{
  content:"☁"; }

.bp3-icon-cloud-download::before{
  content:""; }

.bp3-icon-cloud-upload::before{
  content:""; }

.bp3-icon-code::before{
  content:""; }

.bp3-icon-code-block::before{
  content:""; }

.bp3-icon-cog::before{
  content:""; }

.bp3-icon-collapse-all::before{
  content:""; }

.bp3-icon-column-layout::before{
  content:""; }

.bp3-icon-comment::before{
  content:""; }

.bp3-icon-comparison::before{
  content:""; }

.bp3-icon-compass::before{
  content:""; }

.bp3-icon-compressed::before{
  content:""; }

.bp3-icon-confirm::before{
  content:""; }

.bp3-icon-console::before{
  content:""; }

.bp3-icon-contrast::before{
  content:""; }

.bp3-icon-control::before{
  content:""; }

.bp3-icon-credit-card::before{
  content:""; }

.bp3-icon-cross::before{
  content:"✗"; }

.bp3-icon-crown::before{
  content:""; }

.bp3-icon-cube::before{
  content:""; }

.bp3-icon-cube-add::before{
  content:""; }

.bp3-icon-cube-remove::before{
  content:""; }

.bp3-icon-curved-range-chart::before{
  content:""; }

.bp3-icon-cut::before{
  content:""; }

.bp3-icon-dashboard::before{
  content:""; }

.bp3-icon-data-lineage::before{
  content:""; }

.bp3-icon-database::before{
  content:""; }

.bp3-icon-delete::before{
  content:""; }

.bp3-icon-delta::before{
  content:"Δ"; }

.bp3-icon-derive-column::before{
  content:""; }

.bp3-icon-desktop::before{
  content:""; }

.bp3-icon-diagram-tree::before{
  content:""; }

.bp3-icon-direction-left::before{
  content:""; }

.bp3-icon-direction-right::before{
  content:""; }

.bp3-icon-disable::before{
  content:""; }

.bp3-icon-document::before{
  content:""; }

.bp3-icon-document-open::before{
  content:""; }

.bp3-icon-document-share::before{
  content:""; }

.bp3-icon-dollar::before{
  content:"$"; }

.bp3-icon-dot::before{
  content:"•"; }

.bp3-icon-double-caret-horizontal::before{
  content:""; }

.bp3-icon-double-caret-vertical::before{
  content:""; }

.bp3-icon-double-chevron-down::before{
  content:""; }

.bp3-icon-double-chevron-left::before{
  content:""; }

.bp3-icon-double-chevron-right::before{
  content:""; }

.bp3-icon-double-chevron-up::before{
  content:""; }

.bp3-icon-doughnut-chart::before{
  content:""; }

.bp3-icon-download::before{
  content:""; }

.bp3-icon-drag-handle-horizontal::before{
  content:""; }

.bp3-icon-drag-handle-vertical::before{
  content:""; }

.bp3-icon-draw::before{
  content:""; }

.bp3-icon-drive-time::before{
  content:""; }

.bp3-icon-duplicate::before{
  content:""; }

.bp3-icon-edit::before{
  content:"✎"; }

.bp3-icon-eject::before{
  content:"⏏"; }

.bp3-icon-endorsed::before{
  content:""; }

.bp3-icon-envelope::before{
  content:"✉"; }

.bp3-icon-equals::before{
  content:""; }

.bp3-icon-eraser::before{
  content:""; }

.bp3-icon-error::before{
  content:""; }

.bp3-icon-euro::before{
  content:"€"; }

.bp3-icon-exchange::before{
  content:""; }

.bp3-icon-exclude-row::before{
  content:""; }

.bp3-icon-expand-all::before{
  content:""; }

.bp3-icon-export::before{
  content:""; }

.bp3-icon-eye-off::before{
  content:""; }

.bp3-icon-eye-on::before{
  content:""; }

.bp3-icon-eye-open::before{
  content:""; }

.bp3-icon-fast-backward::before{
  content:""; }

.bp3-icon-fast-forward::before{
  content:""; }

.bp3-icon-feed::before{
  content:""; }

.bp3-icon-feed-subscribed::before{
  content:""; }

.bp3-icon-film::before{
  content:""; }

.bp3-icon-filter::before{
  content:""; }

.bp3-icon-filter-keep::before{
  content:""; }

.bp3-icon-filter-list::before{
  content:""; }

.bp3-icon-filter-open::before{
  content:""; }

.bp3-icon-filter-remove::before{
  content:""; }

.bp3-icon-flag::before{
  content:"⚑"; }

.bp3-icon-flame::before{
  content:""; }

.bp3-icon-flash::before{
  content:""; }

.bp3-icon-floppy-disk::before{
  content:""; }

.bp3-icon-flow-branch::before{
  content:""; }

.bp3-icon-flow-end::before{
  content:""; }

.bp3-icon-flow-linear::before{
  content:""; }

.bp3-icon-flow-review::before{
  content:""; }

.bp3-icon-flow-review-branch::before{
  content:""; }

.bp3-icon-flows::before{
  content:""; }

.bp3-icon-folder-close::before{
  content:""; }

.bp3-icon-folder-new::before{
  content:""; }

.bp3-icon-folder-open::before{
  content:""; }

.bp3-icon-folder-shared::before{
  content:""; }

.bp3-icon-folder-shared-open::before{
  content:""; }

.bp3-icon-follower::before{
  content:""; }

.bp3-icon-following::before{
  content:""; }

.bp3-icon-font::before{
  content:""; }

.bp3-icon-fork::before{
  content:""; }

.bp3-icon-form::before{
  content:""; }

.bp3-icon-full-circle::before{
  content:""; }

.bp3-icon-full-stacked-chart::before{
  content:""; }

.bp3-icon-fullscreen::before{
  content:""; }

.bp3-icon-function::before{
  content:""; }

.bp3-icon-gantt-chart::before{
  content:""; }

.bp3-icon-geolocation::before{
  content:""; }

.bp3-icon-geosearch::before{
  content:""; }

.bp3-icon-git-branch::before{
  content:""; }

.bp3-icon-git-commit::before{
  content:""; }

.bp3-icon-git-merge::before{
  content:""; }

.bp3-icon-git-new-branch::before{
  content:""; }

.bp3-icon-git-pull::before{
  content:""; }

.bp3-icon-git-push::before{
  content:""; }

.bp3-icon-git-repo::before{
  content:""; }

.bp3-icon-glass::before{
  content:""; }

.bp3-icon-globe::before{
  content:""; }

.bp3-icon-globe-network::before{
  content:""; }

.bp3-icon-graph::before{
  content:""; }

.bp3-icon-graph-remove::before{
  content:""; }

.bp3-icon-greater-than::before{
  content:""; }

.bp3-icon-greater-than-or-equal-to::before{
  content:""; }

.bp3-icon-grid::before{
  content:""; }

.bp3-icon-grid-view::before{
  content:""; }

.bp3-icon-group-objects::before{
  content:""; }

.bp3-icon-grouped-bar-chart::before{
  content:""; }

.bp3-icon-hand::before{
  content:""; }

.bp3-icon-hand-down::before{
  content:""; }

.bp3-icon-hand-left::before{
  content:""; }

.bp3-icon-hand-right::before{
  content:""; }

.bp3-icon-hand-up::before{
  content:""; }

.bp3-icon-header::before{
  content:""; }

.bp3-icon-header-one::before{
  content:""; }

.bp3-icon-header-two::before{
  content:""; }

.bp3-icon-headset::before{
  content:""; }

.bp3-icon-heart::before{
  content:"♥"; }

.bp3-icon-heart-broken::before{
  content:""; }

.bp3-icon-heat-grid::before{
  content:""; }

.bp3-icon-heatmap::before{
  content:""; }

.bp3-icon-help::before{
  content:"?"; }

.bp3-icon-helper-management::before{
  content:""; }

.bp3-icon-highlight::before{
  content:""; }

.bp3-icon-history::before{
  content:""; }

.bp3-icon-home::before{
  content:"⌂"; }

.bp3-icon-horizontal-bar-chart::before{
  content:""; }

.bp3-icon-horizontal-bar-chart-asc::before{
  content:""; }

.bp3-icon-horizontal-bar-chart-desc::before{
  content:""; }

.bp3-icon-horizontal-distribution::before{
  content:""; }

.bp3-icon-id-number::before{
  content:""; }

.bp3-icon-image-rotate-left::before{
  content:""; }

.bp3-icon-image-rotate-right::before{
  content:""; }

.bp3-icon-import::before{
  content:""; }

.bp3-icon-inbox::before{
  content:""; }

.bp3-icon-inbox-filtered::before{
  content:""; }

.bp3-icon-inbox-geo::before{
  content:""; }

.bp3-icon-inbox-search::before{
  content:""; }

.bp3-icon-inbox-update::before{
  content:""; }

.bp3-icon-info-sign::before{
  content:"ℹ"; }

.bp3-icon-inheritance::before{
  content:""; }

.bp3-icon-inner-join::before{
  content:""; }

.bp3-icon-insert::before{
  content:""; }

.bp3-icon-intersection::before{
  content:""; }

.bp3-icon-ip-address::before{
  content:""; }

.bp3-icon-issue::before{
  content:""; }

.bp3-icon-issue-closed::before{
  content:""; }

.bp3-icon-issue-new::before{
  content:""; }

.bp3-icon-italic::before{
  content:""; }

.bp3-icon-join-table::before{
  content:""; }

.bp3-icon-key::before{
  content:""; }

.bp3-icon-key-backspace::before{
  content:""; }

.bp3-icon-key-command::before{
  content:""; }

.bp3-icon-key-control::before{
  content:""; }

.bp3-icon-key-delete::before{
  content:""; }

.bp3-icon-key-enter::before{
  content:""; }

.bp3-icon-key-escape::before{
  content:""; }

.bp3-icon-key-option::before{
  content:""; }

.bp3-icon-key-shift::before{
  content:""; }

.bp3-icon-key-tab::before{
  content:""; }

.bp3-icon-known-vehicle::before{
  content:""; }

.bp3-icon-label::before{
  content:""; }

.bp3-icon-layer::before{
  content:""; }

.bp3-icon-layers::before{
  content:""; }

.bp3-icon-layout::before{
  content:""; }

.bp3-icon-layout-auto::before{
  content:""; }

.bp3-icon-layout-balloon::before{
  content:""; }

.bp3-icon-layout-circle::before{
  content:""; }

.bp3-icon-layout-grid::before{
  content:""; }

.bp3-icon-layout-group-by::before{
  content:""; }

.bp3-icon-layout-hierarchy::before{
  content:""; }

.bp3-icon-layout-linear::before{
  content:""; }

.bp3-icon-layout-skew-grid::before{
  content:""; }

.bp3-icon-layout-sorted-clusters::before{
  content:""; }

.bp3-icon-learning::before{
  content:""; }

.bp3-icon-left-join::before{
  content:""; }

.bp3-icon-less-than::before{
  content:""; }

.bp3-icon-less-than-or-equal-to::before{
  content:""; }

.bp3-icon-lifesaver::before{
  content:""; }

.bp3-icon-lightbulb::before{
  content:""; }

.bp3-icon-link::before{
  content:""; }

.bp3-icon-list::before{
  content:"☰"; }

.bp3-icon-list-columns::before{
  content:""; }

.bp3-icon-list-detail-view::before{
  content:""; }

.bp3-icon-locate::before{
  content:""; }

.bp3-icon-lock::before{
  content:""; }

.bp3-icon-log-in::before{
  content:""; }

.bp3-icon-log-out::before{
  content:""; }

.bp3-icon-manual::before{
  content:""; }

.bp3-icon-manually-entered-data::before{
  content:""; }

.bp3-icon-map::before{
  content:""; }

.bp3-icon-map-create::before{
  content:""; }

.bp3-icon-map-marker::before{
  content:""; }

.bp3-icon-maximize::before{
  content:""; }

.bp3-icon-media::before{
  content:""; }

.bp3-icon-menu::before{
  content:""; }

.bp3-icon-menu-closed::before{
  content:""; }

.bp3-icon-menu-open::before{
  content:""; }

.bp3-icon-merge-columns::before{
  content:""; }

.bp3-icon-merge-links::before{
  content:""; }

.bp3-icon-minimize::before{
  content:""; }

.bp3-icon-minus::before{
  content:"−"; }

.bp3-icon-mobile-phone::before{
  content:""; }

.bp3-icon-mobile-video::before{
  content:""; }

.bp3-icon-moon::before{
  content:""; }

.bp3-icon-more::before{
  content:""; }

.bp3-icon-mountain::before{
  content:""; }

.bp3-icon-move::before{
  content:""; }

.bp3-icon-mugshot::before{
  content:""; }

.bp3-icon-multi-select::before{
  content:""; }

.bp3-icon-music::before{
  content:""; }

.bp3-icon-new-drawing::before{
  content:""; }

.bp3-icon-new-grid-item::before{
  content:""; }

.bp3-icon-new-layer::before{
  content:""; }

.bp3-icon-new-layers::before{
  content:""; }

.bp3-icon-new-link::before{
  content:""; }

.bp3-icon-new-object::before{
  content:""; }

.bp3-icon-new-person::before{
  content:""; }

.bp3-icon-new-prescription::before{
  content:""; }

.bp3-icon-new-text-box::before{
  content:""; }

.bp3-icon-ninja::before{
  content:""; }

.bp3-icon-not-equal-to::before{
  content:""; }

.bp3-icon-notifications::before{
  content:""; }

.bp3-icon-notifications-updated::before{
  content:""; }

.bp3-icon-numbered-list::before{
  content:""; }

.bp3-icon-numerical::before{
  content:""; }

.bp3-icon-office::before{
  content:""; }

.bp3-icon-offline::before{
  content:""; }

.bp3-icon-oil-field::before{
  content:""; }

.bp3-icon-one-column::before{
  content:""; }

.bp3-icon-outdated::before{
  content:""; }

.bp3-icon-page-layout::before{
  content:""; }

.bp3-icon-panel-stats::before{
  content:""; }

.bp3-icon-panel-table::before{
  content:""; }

.bp3-icon-paperclip::before{
  content:""; }

.bp3-icon-paragraph::before{
  content:""; }

.bp3-icon-path::before{
  content:""; }

.bp3-icon-path-search::before{
  content:""; }

.bp3-icon-pause::before{
  content:""; }

.bp3-icon-people::before{
  content:""; }

.bp3-icon-percentage::before{
  content:""; }

.bp3-icon-person::before{
  content:""; }

.bp3-icon-phone::before{
  content:"☎"; }

.bp3-icon-pie-chart::before{
  content:""; }

.bp3-icon-pin::before{
  content:""; }

.bp3-icon-pivot::before{
  content:""; }

.bp3-icon-pivot-table::before{
  content:""; }

.bp3-icon-play::before{
  content:""; }

.bp3-icon-plus::before{
  content:"+"; }

.bp3-icon-polygon-filter::before{
  content:""; }

.bp3-icon-power::before{
  content:""; }

.bp3-icon-predictive-analysis::before{
  content:""; }

.bp3-icon-prescription::before{
  content:""; }

.bp3-icon-presentation::before{
  content:""; }

.bp3-icon-print::before{
  content:"⎙"; }

.bp3-icon-projects::before{
  content:""; }

.bp3-icon-properties::before{
  content:""; }

.bp3-icon-property::before{
  content:""; }

.bp3-icon-publish-function::before{
  content:""; }

.bp3-icon-pulse::before{
  content:""; }

.bp3-icon-random::before{
  content:""; }

.bp3-icon-record::before{
  content:""; }

.bp3-icon-redo::before{
  content:""; }

.bp3-icon-refresh::before{
  content:""; }

.bp3-icon-regression-chart::before{
  content:""; }

.bp3-icon-remove::before{
  content:""; }

.bp3-icon-remove-column::before{
  content:""; }

.bp3-icon-remove-column-left::before{
  content:""; }

.bp3-icon-remove-column-right::before{
  content:""; }

.bp3-icon-remove-row-bottom::before{
  content:""; }

.bp3-icon-remove-row-top::before{
  content:""; }

.bp3-icon-repeat::before{
  content:""; }

.bp3-icon-reset::before{
  content:""; }

.bp3-icon-resolve::before{
  content:""; }

.bp3-icon-rig::before{
  content:""; }

.bp3-icon-right-join::before{
  content:""; }

.bp3-icon-ring::before{
  content:""; }

.bp3-icon-rotate-document::before{
  content:""; }

.bp3-icon-rotate-page::before{
  content:""; }

.bp3-icon-satellite::before{
  content:""; }

.bp3-icon-saved::before{
  content:""; }

.bp3-icon-scatter-plot::before{
  content:""; }

.bp3-icon-search::before{
  content:""; }

.bp3-icon-search-around::before{
  content:""; }

.bp3-icon-search-template::before{
  content:""; }

.bp3-icon-search-text::before{
  content:""; }

.bp3-icon-segmented-control::before{
  content:""; }

.bp3-icon-select::before{
  content:""; }

.bp3-icon-selection::before{
  content:"⦿"; }

.bp3-icon-send-to::before{
  content:""; }

.bp3-icon-send-to-graph::before{
  content:""; }

.bp3-icon-send-to-map::before{
  content:""; }

.bp3-icon-series-add::before{
  content:""; }

.bp3-icon-series-configuration::before{
  content:""; }

.bp3-icon-series-derived::before{
  content:""; }

.bp3-icon-series-filtered::before{
  content:""; }

.bp3-icon-series-search::before{
  content:""; }

.bp3-icon-settings::before{
  content:""; }

.bp3-icon-share::before{
  content:""; }

.bp3-icon-shield::before{
  content:""; }

.bp3-icon-shop::before{
  content:""; }

.bp3-icon-shopping-cart::before{
  content:""; }

.bp3-icon-signal-search::before{
  content:""; }

.bp3-icon-sim-card::before{
  content:""; }

.bp3-icon-slash::before{
  content:""; }

.bp3-icon-small-cross::before{
  content:""; }

.bp3-icon-small-minus::before{
  content:""; }

.bp3-icon-small-plus::before{
  content:""; }

.bp3-icon-small-tick::before{
  content:""; }

.bp3-icon-snowflake::before{
  content:""; }

.bp3-icon-social-media::before{
  content:""; }

.bp3-icon-sort::before{
  content:""; }

.bp3-icon-sort-alphabetical::before{
  content:""; }

.bp3-icon-sort-alphabetical-desc::before{
  content:""; }

.bp3-icon-sort-asc::before{
  content:""; }

.bp3-icon-sort-desc::before{
  content:""; }

.bp3-icon-sort-numerical::before{
  content:""; }

.bp3-icon-sort-numerical-desc::before{
  content:""; }

.bp3-icon-split-columns::before{
  content:""; }

.bp3-icon-square::before{
  content:""; }

.bp3-icon-stacked-chart::before{
  content:""; }

.bp3-icon-star::before{
  content:"★"; }

.bp3-icon-star-empty::before{
  content:"☆"; }

.bp3-icon-step-backward::before{
  content:""; }

.bp3-icon-step-chart::before{
  content:""; }

.bp3-icon-step-forward::before{
  content:""; }

.bp3-icon-stop::before{
  content:""; }

.bp3-icon-stopwatch::before{
  content:""; }

.bp3-icon-strikethrough::before{
  content:""; }

.bp3-icon-style::before{
  content:""; }

.bp3-icon-swap-horizontal::before{
  content:""; }

.bp3-icon-swap-vertical::before{
  content:""; }

.bp3-icon-symbol-circle::before{
  content:""; }

.bp3-icon-symbol-cross::before{
  content:""; }

.bp3-icon-symbol-diamond::before{
  content:""; }

.bp3-icon-symbol-square::before{
  content:""; }

.bp3-icon-symbol-triangle-down::before{
  content:""; }

.bp3-icon-symbol-triangle-up::before{
  content:""; }

.bp3-icon-tag::before{
  content:""; }

.bp3-icon-take-action::before{
  content:""; }

.bp3-icon-taxi::before{
  content:""; }

.bp3-icon-text-highlight::before{
  content:""; }

.bp3-icon-th::before{
  content:""; }

.bp3-icon-th-derived::before{
  content:""; }

.bp3-icon-th-disconnect::before{
  content:""; }

.bp3-icon-th-filtered::before{
  content:""; }

.bp3-icon-th-list::before{
  content:""; }

.bp3-icon-thumbs-down::before{
  content:""; }

.bp3-icon-thumbs-up::before{
  content:""; }

.bp3-icon-tick::before{
  content:"✓"; }

.bp3-icon-tick-circle::before{
  content:""; }

.bp3-icon-time::before{
  content:"⏲"; }

.bp3-icon-timeline-area-chart::before{
  content:""; }

.bp3-icon-timeline-bar-chart::before{
  content:""; }

.bp3-icon-timeline-events::before{
  content:""; }

.bp3-icon-timeline-line-chart::before{
  content:""; }

.bp3-icon-tint::before{
  content:""; }

.bp3-icon-torch::before{
  content:""; }

.bp3-icon-tractor::before{
  content:""; }

.bp3-icon-train::before{
  content:""; }

.bp3-icon-translate::before{
  content:""; }

.bp3-icon-trash::before{
  content:""; }

.bp3-icon-tree::before{
  content:""; }

.bp3-icon-trending-down::before{
  content:""; }

.bp3-icon-trending-up::before{
  content:""; }

.bp3-icon-truck::before{
  content:""; }

.bp3-icon-two-columns::before{
  content:""; }

.bp3-icon-unarchive::before{
  content:""; }

.bp3-icon-underline::before{
  content:"⎁"; }

.bp3-icon-undo::before{
  content:"⎌"; }

.bp3-icon-ungroup-objects::before{
  content:""; }

.bp3-icon-unknown-vehicle::before{
  content:""; }

.bp3-icon-unlock::before{
  content:""; }

.bp3-icon-unpin::before{
  content:""; }

.bp3-icon-unresolve::before{
  content:""; }

.bp3-icon-updated::before{
  content:""; }

.bp3-icon-upload::before{
  content:""; }

.bp3-icon-user::before{
  content:""; }

.bp3-icon-variable::before{
  content:""; }

.bp3-icon-vertical-bar-chart-asc::before{
  content:""; }

.bp3-icon-vertical-bar-chart-desc::before{
  content:""; }

.bp3-icon-vertical-distribution::before{
  content:""; }

.bp3-icon-video::before{
  content:""; }

.bp3-icon-volume-down::before{
  content:""; }

.bp3-icon-volume-off::before{
  content:""; }

.bp3-icon-volume-up::before{
  content:""; }

.bp3-icon-walk::before{
  content:""; }

.bp3-icon-warning-sign::before{
  content:""; }

.bp3-icon-waterfall-chart::before{
  content:""; }

.bp3-icon-widget::before{
  content:""; }

.bp3-icon-widget-button::before{
  content:""; }

.bp3-icon-widget-footer::before{
  content:""; }

.bp3-icon-widget-header::before{
  content:""; }

.bp3-icon-wrench::before{
  content:""; }

.bp3-icon-zoom-in::before{
  content:""; }

.bp3-icon-zoom-out::before{
  content:""; }

.bp3-icon-zoom-to-fit::before{
  content:""; }
.bp3-submenu > .bp3-popover-wrapper{
  display:block; }

.bp3-submenu .bp3-popover-target{
  display:block; }

.bp3-submenu.bp3-popover{
  -webkit-box-shadow:none;
          box-shadow:none;
  padding:0 5px; }
  .bp3-submenu.bp3-popover > .bp3-popover-content{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-submenu.bp3-popover, .bp3-submenu.bp3-popover.bp3-dark{
    -webkit-box-shadow:none;
            box-shadow:none; }
    .bp3-dark .bp3-submenu.bp3-popover > .bp3-popover-content, .bp3-submenu.bp3-popover.bp3-dark > .bp3-popover-content{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
.bp3-menu{
  margin:0;
  border-radius:3px;
  background:#ffffff;
  min-width:180px;
  padding:5px;
  list-style:none;
  text-align:left;
  color:#182026; }

.bp3-menu-divider{
  display:block;
  margin:5px;
  border-top:1px solid rgba(16, 22, 26, 0.15); }
  .bp3-dark .bp3-menu-divider{
    border-top-color:rgba(255, 255, 255, 0.15); }

.bp3-menu-item{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  border-radius:2px;
  padding:5px 7px;
  text-decoration:none;
  line-height:20px;
  color:inherit;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-menu-item > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-menu-item > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-menu-item::before,
  .bp3-menu-item > *{
    margin-right:7px; }
  .bp3-menu-item:empty::before,
  .bp3-menu-item > :last-child{
    margin-right:0; }
  .bp3-menu-item > .bp3-fill{
    word-break:break-word; }
  .bp3-menu-item:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
    background-color:rgba(167, 182, 194, 0.3);
    cursor:pointer;
    text-decoration:none; }
  .bp3-menu-item.bp3-disabled{
    background-color:inherit;
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-dark .bp3-menu-item{
    color:inherit; }
    .bp3-dark .bp3-menu-item:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
      background-color:rgba(138, 155, 168, 0.15);
      color:inherit; }
    .bp3-dark .bp3-menu-item.bp3-disabled{
      background-color:inherit;
      color:rgba(167, 182, 194, 0.6); }
  .bp3-menu-item.bp3-intent-primary{
    color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-primary::before, .bp3-menu-item.bp3-intent-primary::after,
    .bp3-menu-item.bp3-intent-primary .bp3-menu-item-label{
      color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-menu-item.bp3-intent-primary.bp3-active{
      background-color:#137cbd; }
    .bp3-menu-item.bp3-intent-primary:active{
      background-color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-menu-item.bp3-intent-primary:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-menu-item.bp3-intent-primary:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-primary:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-primary:active, .bp3-menu-item.bp3-intent-primary:active::before, .bp3-menu-item.bp3-intent-primary:active::after,
    .bp3-menu-item.bp3-intent-primary:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-primary.bp3-active, .bp3-menu-item.bp3-intent-primary.bp3-active::before, .bp3-menu-item.bp3-intent-primary.bp3-active::after,
    .bp3-menu-item.bp3-intent-primary.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-success{
    color:#0d8050; }
    .bp3-menu-item.bp3-intent-success .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-success::before, .bp3-menu-item.bp3-intent-success::after,
    .bp3-menu-item.bp3-intent-success .bp3-menu-item-label{
      color:#0d8050; }
    .bp3-menu-item.bp3-intent-success:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-menu-item.bp3-intent-success.bp3-active{
      background-color:#0f9960; }
    .bp3-menu-item.bp3-intent-success:active{
      background-color:#0d8050; }
    .bp3-menu-item.bp3-intent-success:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-menu-item.bp3-intent-success:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-menu-item.bp3-intent-success:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-success:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-success:active, .bp3-menu-item.bp3-intent-success:active::before, .bp3-menu-item.bp3-intent-success:active::after,
    .bp3-menu-item.bp3-intent-success:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-success.bp3-active, .bp3-menu-item.bp3-intent-success.bp3-active::before, .bp3-menu-item.bp3-intent-success.bp3-active::after,
    .bp3-menu-item.bp3-intent-success.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-warning{
    color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-warning::before, .bp3-menu-item.bp3-intent-warning::after,
    .bp3-menu-item.bp3-intent-warning .bp3-menu-item-label{
      color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-menu-item.bp3-intent-warning.bp3-active{
      background-color:#d9822b; }
    .bp3-menu-item.bp3-intent-warning:active{
      background-color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-menu-item.bp3-intent-warning:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-menu-item.bp3-intent-warning:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-warning:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-warning:active, .bp3-menu-item.bp3-intent-warning:active::before, .bp3-menu-item.bp3-intent-warning:active::after,
    .bp3-menu-item.bp3-intent-warning:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-warning.bp3-active, .bp3-menu-item.bp3-intent-warning.bp3-active::before, .bp3-menu-item.bp3-intent-warning.bp3-active::after,
    .bp3-menu-item.bp3-intent-warning.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-danger{
    color:#c23030; }
    .bp3-menu-item.bp3-intent-danger .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-danger::before, .bp3-menu-item.bp3-intent-danger::after,
    .bp3-menu-item.bp3-intent-danger .bp3-menu-item-label{
      color:#c23030; }
    .bp3-menu-item.bp3-intent-danger:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-menu-item.bp3-intent-danger.bp3-active{
      background-color:#db3737; }
    .bp3-menu-item.bp3-intent-danger:active{
      background-color:#c23030; }
    .bp3-menu-item.bp3-intent-danger:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-menu-item.bp3-intent-danger:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-menu-item.bp3-intent-danger:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-danger:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-danger:active, .bp3-menu-item.bp3-intent-danger:active::before, .bp3-menu-item.bp3-intent-danger:active::after,
    .bp3-menu-item.bp3-intent-danger:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-danger.bp3-active, .bp3-menu-item.bp3-intent-danger.bp3-active::before, .bp3-menu-item.bp3-intent-danger.bp3-active::after,
    .bp3-menu-item.bp3-intent-danger.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item::before{
    line-height:1;
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-weight:400;
    font-style:normal;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    margin-right:7px; }
  .bp3-menu-item::before,
  .bp3-menu-item > .bp3-icon{
    margin-top:2px;
    color:#5c7080; }
  .bp3-menu-item .bp3-menu-item-label{
    color:#5c7080; }
  .bp3-menu-item:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
    color:inherit; }
  .bp3-menu-item.bp3-active, .bp3-menu-item:active{
    background-color:rgba(115, 134, 148, 0.3); }
  .bp3-menu-item.bp3-disabled{
    outline:none !important;
    background-color:inherit !important;
    cursor:not-allowed !important;
    color:rgba(92, 112, 128, 0.6) !important; }
    .bp3-menu-item.bp3-disabled::before,
    .bp3-menu-item.bp3-disabled > .bp3-icon,
    .bp3-menu-item.bp3-disabled .bp3-menu-item-label{
      color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-large .bp3-menu-item{
    padding:9px 7px;
    line-height:22px;
    font-size:16px; }
    .bp3-large .bp3-menu-item .bp3-icon{
      margin-top:3px; }
    .bp3-large .bp3-menu-item::before{
      line-height:1;
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-weight:400;
      font-style:normal;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased;
      margin-top:1px;
      margin-right:10px; }

button.bp3-menu-item{
  border:none;
  background:none;
  width:100%;
  text-align:left; }
.bp3-menu-header{
  display:block;
  margin:5px;
  border-top:1px solid rgba(16, 22, 26, 0.15);
  cursor:default;
  padding-left:2px; }
  .bp3-dark .bp3-menu-header{
    border-top-color:rgba(255, 255, 255, 0.15); }
  .bp3-menu-header:first-of-type{
    border-top:none; }
  .bp3-menu-header > h6{
    color:#182026;
    font-weight:600;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    margin:0;
    padding:10px 7px 0 1px;
    line-height:17px; }
    .bp3-dark .bp3-menu-header > h6{
      color:#f5f8fa; }
  .bp3-menu-header:first-of-type > h6{
    padding-top:0; }
  .bp3-large .bp3-menu-header > h6{
    padding-top:15px;
    padding-bottom:5px;
    font-size:18px; }
  .bp3-large .bp3-menu-header:first-of-type > h6{
    padding-top:0; }

.bp3-dark .bp3-menu{
  background:#30404d;
  color:#f5f8fa; }

.bp3-dark .bp3-menu-item.bp3-intent-primary{
  color:#48aff0; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary .bp3-icon{
    color:inherit; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary::before, .bp3-dark .bp3-menu-item.bp3-intent-primary::after,
  .bp3-dark .bp3-menu-item.bp3-intent-primary .bp3-menu-item-label{
    color:#48aff0; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active{
    background-color:#137cbd; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary:active{
    background-color:#106ba3; }
  .bp3-dark .bp3-menu-item.bp3-intent-primary:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-primary:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-primary:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after,
  .bp3-dark .bp3-menu-item.bp3-intent-primary:hover .bp3-menu-item-label,
  .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label,
  .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-primary:active, .bp3-dark .bp3-menu-item.bp3-intent-primary:active::before, .bp3-dark .bp3-menu-item.bp3-intent-primary:active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-primary:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active .bp3-menu-item-label{
    color:#ffffff; }

.bp3-dark .bp3-menu-item.bp3-intent-success{
  color:#3dcc91; }
  .bp3-dark .bp3-menu-item.bp3-intent-success .bp3-icon{
    color:inherit; }
  .bp3-dark .bp3-menu-item.bp3-intent-success::before, .bp3-dark .bp3-menu-item.bp3-intent-success::after,
  .bp3-dark .bp3-menu-item.bp3-intent-success .bp3-menu-item-label{
    color:#3dcc91; }
  .bp3-dark .bp3-menu-item.bp3-intent-success:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active{
    background-color:#0f9960; }
  .bp3-dark .bp3-menu-item.bp3-intent-success:active{
    background-color:#0d8050; }
  .bp3-dark .bp3-menu-item.bp3-intent-success:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-success:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-success:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after,
  .bp3-dark .bp3-menu-item.bp3-intent-success:hover .bp3-menu-item-label,
  .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label,
  .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-success:active, .bp3-dark .bp3-menu-item.bp3-intent-success:active::before, .bp3-dark .bp3-menu-item.bp3-intent-success:active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-success:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active .bp3-menu-item-label{
    color:#ffffff; }

.bp3-dark .bp3-menu-item.bp3-intent-warning{
  color:#ffb366; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning .bp3-icon{
    color:inherit; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning::before, .bp3-dark .bp3-menu-item.bp3-intent-warning::after,
  .bp3-dark .bp3-menu-item.bp3-intent-warning .bp3-menu-item-label{
    color:#ffb366; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active{
    background-color:#d9822b; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning:active{
    background-color:#bf7326; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-warning:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-warning:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after,
  .bp3-dark .bp3-menu-item.bp3-intent-warning:hover .bp3-menu-item-label,
  .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label,
  .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-warning:active, .bp3-dark .bp3-menu-item.bp3-intent-warning:active::before, .bp3-dark .bp3-menu-item.bp3-intent-warning:active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-warning:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active .bp3-menu-item-label{
    color:#ffffff; }

.bp3-dark .bp3-menu-item.bp3-intent-danger{
  color:#ff7373; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger .bp3-icon{
    color:inherit; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger::before, .bp3-dark .bp3-menu-item.bp3-intent-danger::after,
  .bp3-dark .bp3-menu-item.bp3-intent-danger .bp3-menu-item-label{
    color:#ff7373; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active{
    background-color:#db3737; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger:active{
    background-color:#c23030; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-danger:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-danger:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after,
  .bp3-dark .bp3-menu-item.bp3-intent-danger:hover .bp3-menu-item-label,
  .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label,
  .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-danger:active, .bp3-dark .bp3-menu-item.bp3-intent-danger:active::before, .bp3-dark .bp3-menu-item.bp3-intent-danger:active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-danger:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active::after,
  .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active .bp3-menu-item-label{
    color:#ffffff; }

.bp3-dark .bp3-menu-item::before,
.bp3-dark .bp3-menu-item > .bp3-icon{
  color:#a7b6c2; }

.bp3-dark .bp3-menu-item .bp3-menu-item-label{
  color:#a7b6c2; }

.bp3-dark .bp3-menu-item.bp3-active, .bp3-dark .bp3-menu-item:active{
  background-color:rgba(138, 155, 168, 0.3); }

.bp3-dark .bp3-menu-item.bp3-disabled{
  color:rgba(167, 182, 194, 0.6) !important; }
  .bp3-dark .bp3-menu-item.bp3-disabled::before,
  .bp3-dark .bp3-menu-item.bp3-disabled > .bp3-icon,
  .bp3-dark .bp3-menu-item.bp3-disabled .bp3-menu-item-label{
    color:rgba(167, 182, 194, 0.6) !important; }

.bp3-dark .bp3-menu-divider,
.bp3-dark .bp3-menu-header{
  border-color:rgba(255, 255, 255, 0.15); }

.bp3-dark .bp3-menu-header > h6{
  color:#f5f8fa; }

.bp3-label .bp3-menu{
  margin-top:5px; }
.bp3-navbar{
  position:relative;
  z-index:10;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  background-color:#ffffff;
  width:100%;
  height:50px;
  padding:0 15px; }
  .bp3-navbar.bp3-dark,
  .bp3-dark .bp3-navbar{
    background-color:#394b59; }
  .bp3-navbar.bp3-dark{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-navbar{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-navbar.bp3-fixed-top{
    position:fixed;
    top:0;
    right:0;
    left:0; }

.bp3-navbar-heading{
  margin-right:15px;
  font-size:16px; }

.bp3-navbar-group{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  height:50px; }
  .bp3-navbar-group.bp3-align-left{
    float:left; }
  .bp3-navbar-group.bp3-align-right{
    float:right; }

.bp3-navbar-divider{
  margin:0 10px;
  border-left:1px solid rgba(16, 22, 26, 0.15);
  height:20px; }
  .bp3-dark .bp3-navbar-divider{
    border-left-color:rgba(255, 255, 255, 0.15); }
.bp3-non-ideal-state{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  width:100%;
  height:100%;
  text-align:center; }
  .bp3-non-ideal-state > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-non-ideal-state > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-non-ideal-state::before,
  .bp3-non-ideal-state > *{
    margin-bottom:20px; }
  .bp3-non-ideal-state:empty::before,
  .bp3-non-ideal-state > :last-child{
    margin-bottom:0; }
  .bp3-non-ideal-state > *{
    max-width:400px; }

.bp3-non-ideal-state-visual{
  color:rgba(92, 112, 128, 0.6);
  font-size:60px; }
  .bp3-dark .bp3-non-ideal-state-visual{
    color:rgba(167, 182, 194, 0.6); }

.bp3-overflow-list{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-wrap:nowrap;
      flex-wrap:nowrap;
  min-width:0; }

.bp3-overflow-list-spacer{
  -ms-flex-negative:1;
      flex-shrink:1;
  width:1px; }

body.bp3-overlay-open{
  overflow:hidden; }

.bp3-overlay{
  position:static;
  top:0;
  right:0;
  bottom:0;
  left:0;
  z-index:20; }
  .bp3-overlay:not(.bp3-overlay-open){
    pointer-events:none; }
  .bp3-overlay.bp3-overlay-container{
    position:fixed;
    overflow:hidden; }
    .bp3-overlay.bp3-overlay-container.bp3-overlay-inline{
      position:absolute; }
  .bp3-overlay.bp3-overlay-scroll-container{
    position:fixed;
    overflow:auto; }
    .bp3-overlay.bp3-overlay-scroll-container.bp3-overlay-inline{
      position:absolute; }
  .bp3-overlay.bp3-overlay-inline{
    display:inline;
    overflow:visible; }

.bp3-overlay-content{
  position:fixed;
  z-index:20; }
  .bp3-overlay-inline .bp3-overlay-content,
  .bp3-overlay-scroll-container .bp3-overlay-content{
    position:absolute; }

.bp3-overlay-backdrop{
  position:fixed;
  top:0;
  right:0;
  bottom:0;
  left:0;
  opacity:1;
  z-index:20;
  background-color:rgba(16, 22, 26, 0.7);
  overflow:auto;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-overlay-backdrop.bp3-overlay-enter, .bp3-overlay-backdrop.bp3-overlay-appear{
    opacity:0; }
  .bp3-overlay-backdrop.bp3-overlay-enter-active, .bp3-overlay-backdrop.bp3-overlay-appear-active{
    opacity:1;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-overlay-backdrop.bp3-overlay-exit{
    opacity:1; }
  .bp3-overlay-backdrop.bp3-overlay-exit-active{
    opacity:0;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-overlay-backdrop:focus{
    outline:none; }
  .bp3-overlay-inline .bp3-overlay-backdrop{
    position:absolute; }
.bp3-panel-stack{
  position:relative;
  overflow:hidden; }

.bp3-panel-stack-header{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-negative:0;
      flex-shrink:0;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  z-index:1;
  -webkit-box-shadow:0 1px rgba(16, 22, 26, 0.15);
          box-shadow:0 1px rgba(16, 22, 26, 0.15);
  height:30px; }
  .bp3-dark .bp3-panel-stack-header{
    -webkit-box-shadow:0 1px rgba(255, 255, 255, 0.15);
            box-shadow:0 1px rgba(255, 255, 255, 0.15); }
  .bp3-panel-stack-header > span{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-flex:1;
        -ms-flex:1;
            flex:1;
    -webkit-box-align:stretch;
        -ms-flex-align:stretch;
            align-items:stretch; }
  .bp3-panel-stack-header .bp3-heading{
    margin:0 5px; }

.bp3-button.bp3-panel-stack-header-back{
  margin-left:5px;
  padding-left:0;
  white-space:nowrap; }
  .bp3-button.bp3-panel-stack-header-back .bp3-icon{
    margin:0 2px; }

.bp3-panel-stack-view{
  position:absolute;
  top:0;
  right:0;
  bottom:0;
  left:0;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin-right:-1px;
  border-right:1px solid rgba(16, 22, 26, 0.15);
  background-color:#ffffff;
  overflow-y:auto; }
  .bp3-dark .bp3-panel-stack-view{
    background-color:#30404d; }

.bp3-panel-stack-push .bp3-panel-stack-enter, .bp3-panel-stack-push .bp3-panel-stack-appear{
  -webkit-transform:translateX(100%);
          transform:translateX(100%);
  opacity:0; }

.bp3-panel-stack-push .bp3-panel-stack-enter-active, .bp3-panel-stack-push .bp3-panel-stack-appear-active{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease;
  -webkit-transition-delay:0;
          transition-delay:0; }

.bp3-panel-stack-push .bp3-panel-stack-exit{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1; }

.bp3-panel-stack-push .bp3-panel-stack-exit-active{
  -webkit-transform:translateX(-50%);
          transform:translateX(-50%);
  opacity:0;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease;
  -webkit-transition-delay:0;
          transition-delay:0; }

.bp3-panel-stack-pop .bp3-panel-stack-enter, .bp3-panel-stack-pop .bp3-panel-stack-appear{
  -webkit-transform:translateX(-50%);
          transform:translateX(-50%);
  opacity:0; }

.bp3-panel-stack-pop .bp3-panel-stack-enter-active, .bp3-panel-stack-pop .bp3-panel-stack-appear-active{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease;
  -webkit-transition-delay:0;
          transition-delay:0; }

.bp3-panel-stack-pop .bp3-panel-stack-exit{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1; }

.bp3-panel-stack-pop .bp3-panel-stack-exit-active{
  -webkit-transform:translateX(100%);
          transform:translateX(100%);
  opacity:0;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease;
  -webkit-transition-delay:0;
          transition-delay:0; }
.bp3-popover{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  -webkit-transform:scale(1);
          transform:scale(1);
  display:inline-block;
  z-index:20;
  border-radius:3px; }
  .bp3-popover .bp3-popover-arrow{
    position:absolute;
    width:30px;
    height:30px; }
    .bp3-popover .bp3-popover-arrow::before{
      margin:5px;
      width:20px;
      height:20px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover{
    margin-top:-17px;
    margin-bottom:17px; }
    .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow{
      bottom:-11px; }
      .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(-90deg);
                transform:rotate(-90deg); }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover{
    margin-left:17px; }
    .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow{
      left:-11px; }
      .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(0);
                transform:rotate(0); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover{
    margin-top:17px; }
    .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow{
      top:-11px; }
      .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(90deg);
                transform:rotate(90deg); }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover{
    margin-right:17px;
    margin-left:-17px; }
    .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow{
      right:-11px; }
      .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(180deg);
                transform:rotate(180deg); }
  .bp3-tether-element-attached-middle > .bp3-popover > .bp3-popover-arrow{
    top:50%;
    -webkit-transform:translateY(-50%);
            transform:translateY(-50%); }
  .bp3-tether-element-attached-center > .bp3-popover > .bp3-popover-arrow{
    right:50%;
    -webkit-transform:translateX(50%);
            transform:translateX(50%); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow{
    top:-0.3934px; }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow{
    right:-0.3934px; }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow{
    left:-0.3934px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow{
    bottom:-0.3934px; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:top left;
            transform-origin:top left; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:top center;
            transform-origin:top center; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:top right;
            transform-origin:top right; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:center left;
            transform-origin:center left; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:center center;
            transform-origin:center center; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:center right;
            transform-origin:center right; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:bottom left;
            transform-origin:bottom left; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:bottom center;
            transform-origin:bottom center; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:bottom right;
            transform-origin:bottom right; }
  .bp3-popover .bp3-popover-content{
    background:#ffffff;
    color:inherit; }
  .bp3-popover .bp3-popover-arrow::before{
    -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2);
            box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2); }
  .bp3-popover .bp3-popover-arrow-border{
    fill:#10161a;
    fill-opacity:0.1; }
  .bp3-popover .bp3-popover-arrow-fill{
    fill:#ffffff; }
  .bp3-popover-enter > .bp3-popover, .bp3-popover-appear > .bp3-popover{
    -webkit-transform:scale(0.3);
            transform:scale(0.3); }
  .bp3-popover-enter-active > .bp3-popover, .bp3-popover-appear-active > .bp3-popover{
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-popover-exit > .bp3-popover{
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-popover-exit-active > .bp3-popover{
    -webkit-transform:scale(0.3);
            transform:scale(0.3);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-popover .bp3-popover-content{
    position:relative;
    border-radius:3px; }
  .bp3-popover.bp3-popover-content-sizing .bp3-popover-content{
    max-width:350px;
    padding:20px; }
  .bp3-popover-target + .bp3-overlay .bp3-popover.bp3-popover-content-sizing{
    width:350px; }
  .bp3-popover.bp3-minimal{
    margin:0 !important; }
    .bp3-popover.bp3-minimal .bp3-popover-arrow{
      display:none; }
    .bp3-popover.bp3-minimal.bp3-popover{
      -webkit-transform:scale(1);
              transform:scale(1); }
      .bp3-popover-enter > .bp3-popover.bp3-minimal.bp3-popover, .bp3-popover-appear > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1); }
      .bp3-popover-enter-active > .bp3-popover.bp3-minimal.bp3-popover, .bp3-popover-appear-active > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1);
        -webkit-transition-property:-webkit-transform;
        transition-property:-webkit-transform;
        transition-property:transform;
        transition-property:transform, -webkit-transform;
        -webkit-transition-duration:100ms;
                transition-duration:100ms;
        -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
                transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
        -webkit-transition-delay:0;
                transition-delay:0; }
      .bp3-popover-exit > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1); }
      .bp3-popover-exit-active > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1);
        -webkit-transition-property:-webkit-transform;
        transition-property:-webkit-transform;
        transition-property:transform;
        transition-property:transform, -webkit-transform;
        -webkit-transition-duration:100ms;
                transition-duration:100ms;
        -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
                transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
        -webkit-transition-delay:0;
                transition-delay:0; }
  .bp3-popover.bp3-dark,
  .bp3-dark .bp3-popover{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
    .bp3-popover.bp3-dark .bp3-popover-content,
    .bp3-dark .bp3-popover .bp3-popover-content{
      background:#30404d;
      color:inherit; }
    .bp3-popover.bp3-dark .bp3-popover-arrow::before,
    .bp3-dark .bp3-popover .bp3-popover-arrow::before{
      -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4);
              box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4); }
    .bp3-popover.bp3-dark .bp3-popover-arrow-border,
    .bp3-dark .bp3-popover .bp3-popover-arrow-border{
      fill:#10161a;
      fill-opacity:0.2; }
    .bp3-popover.bp3-dark .bp3-popover-arrow-fill,
    .bp3-dark .bp3-popover .bp3-popover-arrow-fill{
      fill:#30404d; }

.bp3-popover-arrow::before{
  display:block;
  position:absolute;
  -webkit-transform:rotate(45deg);
          transform:rotate(45deg);
  border-radius:2px;
  content:""; }

.bp3-tether-pinned .bp3-popover-arrow{
  display:none; }

.bp3-popover-backdrop{
  background:rgba(255, 255, 255, 0); }

.bp3-transition-container{
  opacity:1;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  z-index:20; }
  .bp3-transition-container.bp3-popover-enter, .bp3-transition-container.bp3-popover-appear{
    opacity:0; }
  .bp3-transition-container.bp3-popover-enter-active, .bp3-transition-container.bp3-popover-appear-active{
    opacity:1;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-transition-container.bp3-popover-exit{
    opacity:1; }
  .bp3-transition-container.bp3-popover-exit-active{
    opacity:0;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-transition-container:focus{
    outline:none; }
  .bp3-transition-container.bp3-popover-leave .bp3-popover-content{
    pointer-events:none; }
  .bp3-transition-container[data-x-out-of-boundaries]{
    display:none; }

span.bp3-popover-target{
  display:inline-block; }

.bp3-popover-wrapper.bp3-fill{
  width:100%; }

.bp3-portal{
  position:absolute;
  top:0;
  right:0;
  left:0; }
@-webkit-keyframes linear-progress-bar-stripes{
  from{
    background-position:0 0; }
  to{
    background-position:30px 0; } }
@keyframes linear-progress-bar-stripes{
  from{
    background-position:0 0; }
  to{
    background-position:30px 0; } }

.bp3-progress-bar{
  display:block;
  position:relative;
  border-radius:40px;
  background:rgba(92, 112, 128, 0.2);
  width:100%;
  height:8px;
  overflow:hidden; }
  .bp3-progress-bar .bp3-progress-meter{
    position:absolute;
    border-radius:40px;
    background:linear-gradient(-45deg, rgba(255, 255, 255, 0.2) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.2) 50%, rgba(255, 255, 255, 0.2) 75%, transparent 75%);
    background-color:rgba(92, 112, 128, 0.8);
    background-size:30px 30px;
    width:100%;
    height:100%;
    -webkit-transition:width 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:width 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-progress-bar:not(.bp3-no-animation):not(.bp3-no-stripes) .bp3-progress-meter{
    animation:linear-progress-bar-stripes 300ms linear infinite reverse; }
  .bp3-progress-bar.bp3-no-stripes .bp3-progress-meter{
    background-image:none; }

.bp3-dark .bp3-progress-bar{
  background:rgba(16, 22, 26, 0.5); }
  .bp3-dark .bp3-progress-bar .bp3-progress-meter{
    background-color:#8a9ba8; }

.bp3-progress-bar.bp3-intent-primary .bp3-progress-meter{
  background-color:#137cbd; }

.bp3-progress-bar.bp3-intent-success .bp3-progress-meter{
  background-color:#0f9960; }

.bp3-progress-bar.bp3-intent-warning .bp3-progress-meter{
  background-color:#d9822b; }

.bp3-progress-bar.bp3-intent-danger .bp3-progress-meter{
  background-color:#db3737; }
@-webkit-keyframes skeleton-glow{
  from{
    border-color:rgba(206, 217, 224, 0.2);
    background:rgba(206, 217, 224, 0.2); }
  to{
    border-color:rgba(92, 112, 128, 0.2);
    background:rgba(92, 112, 128, 0.2); } }
@keyframes skeleton-glow{
  from{
    border-color:rgba(206, 217, 224, 0.2);
    background:rgba(206, 217, 224, 0.2); }
  to{
    border-color:rgba(92, 112, 128, 0.2);
    background:rgba(92, 112, 128, 0.2); } }
.bp3-skeleton{
  border-color:rgba(206, 217, 224, 0.2) !important;
  border-radius:2px;
  -webkit-box-shadow:none !important;
          box-shadow:none !important;
  background:rgba(206, 217, 224, 0.2);
  background-clip:padding-box !important;
  cursor:default;
  color:transparent !important;
  -webkit-animation:1000ms linear infinite alternate skeleton-glow;
          animation:1000ms linear infinite alternate skeleton-glow;
  pointer-events:none;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-skeleton::before, .bp3-skeleton::after,
  .bp3-skeleton *{
    visibility:hidden !important; }
.bp3-slider{
  width:100%;
  min-width:150px;
  height:40px;
  position:relative;
  outline:none;
  cursor:default;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-slider:hover{
    cursor:pointer; }
  .bp3-slider:active{
    cursor:-webkit-grabbing;
    cursor:grabbing; }
  .bp3-slider.bp3-disabled{
    opacity:0.5;
    cursor:not-allowed; }
  .bp3-slider.bp3-slider-unlabeled{
    height:16px; }

.bp3-slider-track,
.bp3-slider-progress{
  top:5px;
  right:0;
  left:0;
  height:6px;
  position:absolute; }

.bp3-slider-track{
  border-radius:3px;
  overflow:hidden; }

.bp3-slider-progress{
  background:rgba(92, 112, 128, 0.2); }
  .bp3-dark .bp3-slider-progress{
    background:rgba(16, 22, 26, 0.5); }
  .bp3-slider-progress.bp3-intent-primary{
    background-color:#137cbd; }
  .bp3-slider-progress.bp3-intent-success{
    background-color:#0f9960; }
  .bp3-slider-progress.bp3-intent-warning{
    background-color:#d9822b; }
  .bp3-slider-progress.bp3-intent-danger{
    background-color:#db3737; }

.bp3-slider-handle{
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
  background-color:#f5f8fa;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
  color:#182026;
  position:absolute;
  top:0;
  left:0;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
  cursor:pointer;
  width:16px;
  height:16px; }
  .bp3-slider-handle:hover{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#ebf1f5; }
  .bp3-slider-handle:active, .bp3-slider-handle.bp3-active{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#d8e1e8;
    background-image:none; }
  .bp3-slider-handle:disabled, .bp3-slider-handle.bp3-disabled{
    outline:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    background-color:rgba(206, 217, 224, 0.5);
    background-image:none;
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
    .bp3-slider-handle:disabled.bp3-active, .bp3-slider-handle:disabled.bp3-active:hover, .bp3-slider-handle.bp3-disabled.bp3-active, .bp3-slider-handle.bp3-disabled.bp3-active:hover{
      background:rgba(206, 217, 224, 0.7); }
  .bp3-slider-handle:focus{
    z-index:1; }
  .bp3-slider-handle:hover{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    background-clip:padding-box;
    background-color:#ebf1f5;
    z-index:2;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
    cursor:-webkit-grab;
    cursor:grab; }
  .bp3-slider-handle.bp3-active{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    background-color:#d8e1e8;
    background-image:none;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 1px rgba(16, 22, 26, 0.1);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 1px rgba(16, 22, 26, 0.1);
    cursor:-webkit-grabbing;
    cursor:grabbing; }
  .bp3-disabled .bp3-slider-handle{
    -webkit-box-shadow:none;
            box-shadow:none;
    background:#bfccd6;
    pointer-events:none; }
  .bp3-dark .bp3-slider-handle{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    background-color:#394b59;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
    color:#f5f8fa; }
    .bp3-dark .bp3-slider-handle:hover, .bp3-dark .bp3-slider-handle:active, .bp3-dark .bp3-slider-handle.bp3-active{
      color:#f5f8fa; }
    .bp3-dark .bp3-slider-handle:hover{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      background-color:#30404d; }
    .bp3-dark .bp3-slider-handle:active, .bp3-dark .bp3-slider-handle.bp3-active{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
      background-color:#202b33;
      background-image:none; }
    .bp3-dark .bp3-slider-handle:disabled, .bp3-dark .bp3-slider-handle.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none;
      background-color:rgba(57, 75, 89, 0.5);
      background-image:none;
      color:rgba(167, 182, 194, 0.6); }
      .bp3-dark .bp3-slider-handle:disabled.bp3-active, .bp3-dark .bp3-slider-handle.bp3-disabled.bp3-active{
        background:rgba(57, 75, 89, 0.7); }
    .bp3-dark .bp3-slider-handle .bp3-button-spinner .bp3-spinner-head{
      background:rgba(16, 22, 26, 0.5);
      stroke:#8a9ba8; }
    .bp3-dark .bp3-slider-handle, .bp3-dark .bp3-slider-handle:hover{
      background-color:#394b59; }
    .bp3-dark .bp3-slider-handle.bp3-active{
      background-color:#293742; }
  .bp3-dark .bp3-disabled .bp3-slider-handle{
    border-color:#5c7080;
    -webkit-box-shadow:none;
            box-shadow:none;
    background:#5c7080; }
  .bp3-slider-handle .bp3-slider-label{
    margin-left:8px;
    border-radius:3px;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
    background:#394b59;
    color:#f5f8fa; }
    .bp3-dark .bp3-slider-handle .bp3-slider-label{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
      background:#e1e8ed;
      color:#394b59; }
    .bp3-disabled .bp3-slider-handle .bp3-slider-label{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-slider-handle.bp3-start, .bp3-slider-handle.bp3-end{
    width:8px; }
  .bp3-slider-handle.bp3-start{
    border-top-right-radius:0;
    border-bottom-right-radius:0; }
  .bp3-slider-handle.bp3-end{
    margin-left:8px;
    border-top-left-radius:0;
    border-bottom-left-radius:0; }
    .bp3-slider-handle.bp3-end .bp3-slider-label{
      margin-left:0; }

.bp3-slider-label{
  -webkit-transform:translate(-50%, 20px);
          transform:translate(-50%, 20px);
  display:inline-block;
  position:absolute;
  padding:2px 5px;
  vertical-align:top;
  line-height:1;
  font-size:12px; }

.bp3-slider.bp3-vertical{
  width:40px;
  min-width:40px;
  height:150px; }
  .bp3-slider.bp3-vertical .bp3-slider-track,
  .bp3-slider.bp3-vertical .bp3-slider-progress{
    top:0;
    bottom:0;
    left:5px;
    width:6px;
    height:auto; }
  .bp3-slider.bp3-vertical .bp3-slider-progress{
    top:auto; }
  .bp3-slider.bp3-vertical .bp3-slider-label{
    -webkit-transform:translate(20px, 50%);
            transform:translate(20px, 50%); }
  .bp3-slider.bp3-vertical .bp3-slider-handle{
    top:auto; }
    .bp3-slider.bp3-vertical .bp3-slider-handle .bp3-slider-label{
      margin-top:-8px;
      margin-left:0; }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-end, .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start{
      margin-left:0;
      width:16px;
      height:8px; }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start{
      border-top-left-radius:0;
      border-bottom-right-radius:3px; }
      .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start .bp3-slider-label{
        -webkit-transform:translate(20px);
                transform:translate(20px); }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-end{
      margin-bottom:8px;
      border-top-left-radius:3px;
      border-bottom-left-radius:0;
      border-bottom-right-radius:0; }

@-webkit-keyframes pt-spinner-animation{
  from{
    -webkit-transform:rotate(0deg);
            transform:rotate(0deg); }
  to{
    -webkit-transform:rotate(360deg);
            transform:rotate(360deg); } }

@keyframes pt-spinner-animation{
  from{
    -webkit-transform:rotate(0deg);
            transform:rotate(0deg); }
  to{
    -webkit-transform:rotate(360deg);
            transform:rotate(360deg); } }

.bp3-spinner{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  overflow:visible;
  vertical-align:middle; }
  .bp3-spinner svg{
    display:block; }
  .bp3-spinner path{
    fill-opacity:0; }
  .bp3-spinner .bp3-spinner-head{
    -webkit-transform-origin:center;
            transform-origin:center;
    -webkit-transition:stroke-dashoffset 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:stroke-dashoffset 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    stroke:rgba(92, 112, 128, 0.8);
    stroke-linecap:round; }
  .bp3-spinner .bp3-spinner-track{
    stroke:rgba(92, 112, 128, 0.2); }

.bp3-spinner-animation{
  -webkit-animation:pt-spinner-animation 500ms linear infinite;
          animation:pt-spinner-animation 500ms linear infinite; }
  .bp3-no-spin > .bp3-spinner-animation{
    -webkit-animation:none;
            animation:none; }

.bp3-dark .bp3-spinner .bp3-spinner-head{
  stroke:#8a9ba8; }

.bp3-dark .bp3-spinner .bp3-spinner-track{
  stroke:rgba(16, 22, 26, 0.5); }

.bp3-spinner.bp3-intent-primary .bp3-spinner-head{
  stroke:#137cbd; }

.bp3-spinner.bp3-intent-success .bp3-spinner-head{
  stroke:#0f9960; }

.bp3-spinner.bp3-intent-warning .bp3-spinner-head{
  stroke:#d9822b; }

.bp3-spinner.bp3-intent-danger .bp3-spinner-head{
  stroke:#db3737; }
.bp3-tabs.bp3-vertical{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex; }
  .bp3-tabs.bp3-vertical > .bp3-tab-list{
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column;
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start; }
    .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab{
      border-radius:3px;
      width:100%;
      padding:0 10px; }
      .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab[aria-selected="true"]{
        -webkit-box-shadow:none;
                box-shadow:none;
        background-color:rgba(19, 124, 189, 0.2); }
    .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab-indicator-wrapper .bp3-tab-indicator{
      top:0;
      right:0;
      bottom:0;
      left:0;
      border-radius:3px;
      background-color:rgba(19, 124, 189, 0.2);
      height:auto; }
  .bp3-tabs.bp3-vertical > .bp3-tab-panel{
    margin-top:0;
    padding-left:20px; }

.bp3-tab-list{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  -webkit-box-align:end;
      -ms-flex-align:end;
          align-items:flex-end;
  position:relative;
  margin:0;
  border:none;
  padding:0;
  list-style:none; }
  .bp3-tab-list > *:not(:last-child){
    margin-right:20px; }

.bp3-tab{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  position:relative;
  cursor:pointer;
  max-width:100%;
  vertical-align:top;
  line-height:30px;
  color:#182026;
  font-size:14px; }
  .bp3-tab a{
    display:block;
    text-decoration:none;
    color:inherit; }
  .bp3-tab-indicator-wrapper ~ .bp3-tab{
    -webkit-box-shadow:none !important;
            box-shadow:none !important;
    background-color:transparent !important; }
  .bp3-tab[aria-disabled="true"]{
    cursor:not-allowed;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-tab[aria-selected="true"]{
    border-radius:0;
    -webkit-box-shadow:inset 0 -3px 0 #106ba3;
            box-shadow:inset 0 -3px 0 #106ba3; }
  .bp3-tab[aria-selected="true"], .bp3-tab:not([aria-disabled="true"]):hover{
    color:#106ba3; }
  .bp3-tab:focus{
    -moz-outline-radius:0; }
  .bp3-large > .bp3-tab{
    line-height:40px;
    font-size:16px; }

.bp3-tab-panel{
  margin-top:20px; }
  .bp3-tab-panel[aria-hidden="true"]{
    display:none; }

.bp3-tab-indicator-wrapper{
  position:absolute;
  top:0;
  left:0;
  -webkit-transform:translateX(0), translateY(0);
          transform:translateX(0), translateY(0);
  -webkit-transition:height, width, -webkit-transform;
  transition:height, width, -webkit-transform;
  transition:height, transform, width;
  transition:height, transform, width, -webkit-transform;
  -webkit-transition-duration:200ms;
          transition-duration:200ms;
  -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
          transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
  pointer-events:none; }
  .bp3-tab-indicator-wrapper .bp3-tab-indicator{
    position:absolute;
    right:0;
    bottom:0;
    left:0;
    background-color:#106ba3;
    height:3px; }
  .bp3-tab-indicator-wrapper.bp3-no-animation{
    -webkit-transition:none;
    transition:none; }

.bp3-dark .bp3-tab{
  color:#f5f8fa; }
  .bp3-dark .bp3-tab[aria-disabled="true"]{
    color:rgba(167, 182, 194, 0.6); }
  .bp3-dark .bp3-tab[aria-selected="true"]{
    -webkit-box-shadow:inset 0 -3px 0 #48aff0;
            box-shadow:inset 0 -3px 0 #48aff0; }
  .bp3-dark .bp3-tab[aria-selected="true"], .bp3-dark .bp3-tab:not([aria-disabled="true"]):hover{
    color:#48aff0; }

.bp3-dark .bp3-tab-indicator{
  background-color:#48aff0; }

.bp3-flex-expander{
  -webkit-box-flex:1;
      -ms-flex:1 1;
          flex:1 1; }
.bp3-tag{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  position:relative;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:none;
          box-shadow:none;
  background-color:#5c7080;
  min-width:20px;
  max-width:100%;
  min-height:20px;
  padding:2px 6px;
  line-height:16px;
  color:#f5f8fa;
  font-size:12px; }
  .bp3-tag.bp3-interactive{
    cursor:pointer; }
    .bp3-tag.bp3-interactive:hover{
      background-color:rgba(92, 112, 128, 0.85); }
    .bp3-tag.bp3-interactive.bp3-active, .bp3-tag.bp3-interactive:active{
      background-color:rgba(92, 112, 128, 0.7); }
  .bp3-tag > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-tag > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-tag::before,
  .bp3-tag > *{
    margin-right:4px; }
  .bp3-tag:empty::before,
  .bp3-tag > :last-child{
    margin-right:0; }
  .bp3-tag:focus{
    outline:rgba(19, 124, 189, 0.6) auto 2px;
    outline-offset:0;
    -moz-outline-radius:6px; }
  .bp3-tag.bp3-round{
    border-radius:30px;
    padding-right:8px;
    padding-left:8px; }
  .bp3-dark .bp3-tag{
    background-color:#bfccd6;
    color:#182026; }
    .bp3-dark .bp3-tag.bp3-interactive{
      cursor:pointer; }
      .bp3-dark .bp3-tag.bp3-interactive:hover{
        background-color:rgba(191, 204, 214, 0.85); }
      .bp3-dark .bp3-tag.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-interactive:active{
        background-color:rgba(191, 204, 214, 0.7); }
    .bp3-dark .bp3-tag > .bp3-icon, .bp3-dark .bp3-tag .bp3-icon-standard, .bp3-dark .bp3-tag .bp3-icon-large{
      fill:currentColor; }
  .bp3-tag > .bp3-icon, .bp3-tag .bp3-icon-standard, .bp3-tag .bp3-icon-large{
    fill:#ffffff; }
  .bp3-tag.bp3-large,
  .bp3-large .bp3-tag{
    min-width:30px;
    min-height:30px;
    padding:0 10px;
    line-height:20px;
    font-size:14px; }
    .bp3-tag.bp3-large::before,
    .bp3-tag.bp3-large > *,
    .bp3-large .bp3-tag::before,
    .bp3-large .bp3-tag > *{
      margin-right:7px; }
    .bp3-tag.bp3-large:empty::before,
    .bp3-tag.bp3-large > :last-child,
    .bp3-large .bp3-tag:empty::before,
    .bp3-large .bp3-tag > :last-child{
      margin-right:0; }
    .bp3-tag.bp3-large.bp3-round,
    .bp3-large .bp3-tag.bp3-round{
      padding-right:12px;
      padding-left:12px; }
  .bp3-tag.bp3-intent-primary{
    background:#137cbd;
    color:#ffffff; }
    .bp3-tag.bp3-intent-primary.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-primary.bp3-interactive:hover{
        background-color:rgba(19, 124, 189, 0.85); }
      .bp3-tag.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-primary.bp3-interactive:active{
        background-color:rgba(19, 124, 189, 0.7); }
  .bp3-tag.bp3-intent-success{
    background:#0f9960;
    color:#ffffff; }
    .bp3-tag.bp3-intent-success.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-success.bp3-interactive:hover{
        background-color:rgba(15, 153, 96, 0.85); }
      .bp3-tag.bp3-intent-success.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-success.bp3-interactive:active{
        background-color:rgba(15, 153, 96, 0.7); }
  .bp3-tag.bp3-intent-warning{
    background:#d9822b;
    color:#ffffff; }
    .bp3-tag.bp3-intent-warning.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-warning.bp3-interactive:hover{
        background-color:rgba(217, 130, 43, 0.85); }
      .bp3-tag.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-warning.bp3-interactive:active{
        background-color:rgba(217, 130, 43, 0.7); }
  .bp3-tag.bp3-intent-danger{
    background:#db3737;
    color:#ffffff; }
    .bp3-tag.bp3-intent-danger.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-danger.bp3-interactive:hover{
        background-color:rgba(219, 55, 55, 0.85); }
      .bp3-tag.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-danger.bp3-interactive:active{
        background-color:rgba(219, 55, 55, 0.7); }
  .bp3-tag.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-tag.bp3-minimal > .bp3-icon, .bp3-tag.bp3-minimal .bp3-icon-standard, .bp3-tag.bp3-minimal .bp3-icon-large{
    fill:#5c7080; }
  .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]){
    background-color:rgba(138, 155, 168, 0.2);
    color:#182026; }
    .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:hover{
        background-color:rgba(92, 112, 128, 0.3); }
      .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive.bp3-active, .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:active{
        background-color:rgba(92, 112, 128, 0.4); }
    .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]){
      color:#f5f8fa; }
      .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:hover{
          background-color:rgba(191, 204, 214, 0.3); }
        .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:active{
          background-color:rgba(191, 204, 214, 0.4); }
      .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) > .bp3-icon, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) .bp3-icon-standard, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) .bp3-icon-large{
        fill:#a7b6c2; }
  .bp3-tag.bp3-minimal.bp3-intent-primary{
    background-color:rgba(19, 124, 189, 0.15);
    color:#106ba3; }
    .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:hover{
        background-color:rgba(19, 124, 189, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:active{
        background-color:rgba(19, 124, 189, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-primary > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-primary .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-primary .bp3-icon-large{
      fill:#137cbd; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary{
      background-color:rgba(19, 124, 189, 0.25);
      color:#48aff0; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:hover{
          background-color:rgba(19, 124, 189, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:active{
          background-color:rgba(19, 124, 189, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-success{
    background-color:rgba(15, 153, 96, 0.15);
    color:#0d8050; }
    .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:hover{
        background-color:rgba(15, 153, 96, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:active{
        background-color:rgba(15, 153, 96, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-success > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-success .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-success .bp3-icon-large{
      fill:#0f9960; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success{
      background-color:rgba(15, 153, 96, 0.25);
      color:#3dcc91; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:hover{
          background-color:rgba(15, 153, 96, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:active{
          background-color:rgba(15, 153, 96, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-warning{
    background-color:rgba(217, 130, 43, 0.15);
    color:#bf7326; }
    .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:hover{
        background-color:rgba(217, 130, 43, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:active{
        background-color:rgba(217, 130, 43, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-warning > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-warning .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-warning .bp3-icon-large{
      fill:#d9822b; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning{
      background-color:rgba(217, 130, 43, 0.25);
      color:#ffb366; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:hover{
          background-color:rgba(217, 130, 43, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:active{
          background-color:rgba(217, 130, 43, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-danger{
    background-color:rgba(219, 55, 55, 0.15);
    color:#c23030; }
    .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:hover{
        background-color:rgba(219, 55, 55, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:active{
        background-color:rgba(219, 55, 55, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-danger > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-danger .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-danger .bp3-icon-large{
      fill:#db3737; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger{
      background-color:rgba(219, 55, 55, 0.25);
      color:#ff7373; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:hover{
          background-color:rgba(219, 55, 55, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:active{
          background-color:rgba(219, 55, 55, 0.45); }

.bp3-tag-remove{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  opacity:0.5;
  margin-top:-2px;
  margin-right:-6px !important;
  margin-bottom:-2px;
  border:none;
  background:none;
  cursor:pointer;
  padding:2px;
  padding-left:0;
  color:inherit; }
  .bp3-tag-remove:hover{
    opacity:0.8;
    background:none;
    text-decoration:none; }
  .bp3-tag-remove:active{
    opacity:1; }
  .bp3-tag-remove:empty::before{
    line-height:1;
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-weight:400;
    font-style:normal;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    content:""; }
  .bp3-large .bp3-tag-remove{
    margin-right:-10px !important;
    padding:5px;
    padding-left:0; }
    .bp3-large .bp3-tag-remove:empty::before{
      line-height:1;
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-weight:400;
      font-style:normal; }
.bp3-tag-input{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  cursor:text;
  height:auto;
  min-height:30px;
  padding-right:0;
  padding-left:5px;
  line-height:inherit; }
  .bp3-tag-input > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-tag-input > .bp3-tag-input-values{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-tag-input .bp3-tag-input-icon{
    margin-top:7px;
    margin-right:7px;
    margin-left:2px;
    color:#5c7080; }
  .bp3-tag-input .bp3-tag-input-values{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-orient:horizontal;
    -webkit-box-direction:normal;
        -ms-flex-direction:row;
            flex-direction:row;
    -ms-flex-wrap:wrap;
        flex-wrap:wrap;
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center;
    -ms-flex-item-align:stretch;
        align-self:stretch;
    margin-top:5px;
    margin-right:7px;
    min-width:0; }
    .bp3-tag-input .bp3-tag-input-values > *{
      -webkit-box-flex:0;
          -ms-flex-positive:0;
              flex-grow:0;
      -ms-flex-negative:0;
          flex-shrink:0; }
    .bp3-tag-input .bp3-tag-input-values > .bp3-fill{
      -webkit-box-flex:1;
          -ms-flex-positive:1;
              flex-grow:1;
      -ms-flex-negative:1;
          flex-shrink:1; }
    .bp3-tag-input .bp3-tag-input-values::before,
    .bp3-tag-input .bp3-tag-input-values > *{
      margin-right:5px; }
    .bp3-tag-input .bp3-tag-input-values:empty::before,
    .bp3-tag-input .bp3-tag-input-values > :last-child{
      margin-right:0; }
    .bp3-tag-input .bp3-tag-input-values:first-child .bp3-input-ghost:first-child{
      padding-left:5px; }
    .bp3-tag-input .bp3-tag-input-values > *{
      margin-bottom:5px; }
  .bp3-tag-input .bp3-tag{
    overflow-wrap:break-word; }
    .bp3-tag-input .bp3-tag.bp3-active{
      outline:rgba(19, 124, 189, 0.6) auto 2px;
      outline-offset:0;
      -moz-outline-radius:6px; }
  .bp3-tag-input .bp3-input-ghost{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    width:80px;
    line-height:20px; }
    .bp3-tag-input .bp3-input-ghost:disabled, .bp3-tag-input .bp3-input-ghost.bp3-disabled{
      cursor:not-allowed; }
  .bp3-tag-input .bp3-button,
  .bp3-tag-input .bp3-spinner{
    margin:3px;
    margin-left:0; }
  .bp3-tag-input .bp3-button{
    min-width:24px;
    min-height:24px;
    padding:0 7px; }
  .bp3-tag-input.bp3-large{
    height:auto;
    min-height:40px; }
    .bp3-tag-input.bp3-large::before,
    .bp3-tag-input.bp3-large > *{
      margin-right:10px; }
    .bp3-tag-input.bp3-large:empty::before,
    .bp3-tag-input.bp3-large > :last-child{
      margin-right:0; }
    .bp3-tag-input.bp3-large .bp3-tag-input-icon{
      margin-top:10px;
      margin-left:5px; }
    .bp3-tag-input.bp3-large .bp3-input-ghost{
      line-height:30px; }
    .bp3-tag-input.bp3-large .bp3-button{
      min-width:30px;
      min-height:30px;
      padding:5px 10px;
      margin:5px;
      margin-left:0; }
    .bp3-tag-input.bp3-large .bp3-spinner{
      margin:8px;
      margin-left:0; }
  .bp3-tag-input.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
    background-color:#ffffff; }
    .bp3-tag-input.bp3-active.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-success{
      -webkit-box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-tag-input .bp3-tag-input-icon, .bp3-tag-input.bp3-dark .bp3-tag-input-icon{
    color:#a7b6c2; }
  .bp3-dark .bp3-tag-input .bp3-input-ghost, .bp3-tag-input.bp3-dark .bp3-input-ghost{
    color:#f5f8fa; }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-webkit-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-moz-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost:-ms-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-ms-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::placeholder{
      color:rgba(167, 182, 194, 0.6); }
  .bp3-dark .bp3-tag-input.bp3-active, .bp3-tag-input.bp3-dark.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    background-color:rgba(16, 22, 26, 0.3); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-primary, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-success, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-success{
      -webkit-box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-warning, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-danger, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-input-ghost{
  border:none;
  -webkit-box-shadow:none;
          box-shadow:none;
  background:none;
  padding:0; }
  .bp3-input-ghost::-webkit-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost::-moz-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost:-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost::-ms-input-placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost::placeholder{
    opacity:1;
    color:rgba(92, 112, 128, 0.6); }
  .bp3-input-ghost:focus{
    outline:none !important; }
.bp3-toast{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  position:relative !important;
  margin:20px 0 0;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  background-color:#ffffff;
  min-width:300px;
  max-width:500px;
  pointer-events:all; }
  .bp3-toast.bp3-toast-enter, .bp3-toast.bp3-toast-appear{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px); }
  .bp3-toast.bp3-toast-enter-active, .bp3-toast.bp3-toast-appear-active{
    -webkit-transform:translateY(0);
            transform:translateY(0);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-toast.bp3-toast-enter ~ .bp3-toast, .bp3-toast.bp3-toast-appear ~ .bp3-toast{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px); }
  .bp3-toast.bp3-toast-enter-active ~ .bp3-toast, .bp3-toast.bp3-toast-appear-active ~ .bp3-toast{
    -webkit-transform:translateY(0);
            transform:translateY(0);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-toast.bp3-toast-exit{
    opacity:1;
    -webkit-filter:blur(0);
            filter:blur(0); }
  .bp3-toast.bp3-toast-exit-active{
    opacity:0;
    -webkit-filter:blur(10px);
            filter:blur(10px);
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:opacity, filter;
    transition-property:opacity, filter, -webkit-filter;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-toast.bp3-toast-exit ~ .bp3-toast{
    -webkit-transform:translateY(0);
            transform:translateY(0); }
  .bp3-toast.bp3-toast-exit-active ~ .bp3-toast{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:50ms;
            transition-delay:50ms; }
  .bp3-toast .bp3-button-group{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    padding:5px;
    padding-left:0; }
  .bp3-toast > .bp3-icon{
    margin:12px;
    margin-right:0;
    color:#5c7080; }
  .bp3-toast.bp3-dark,
  .bp3-dark .bp3-toast{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
    background-color:#394b59; }
    .bp3-toast.bp3-dark > .bp3-icon,
    .bp3-dark .bp3-toast > .bp3-icon{
      color:#a7b6c2; }
  .bp3-toast[class*="bp3-intent-"] a{
    color:rgba(255, 255, 255, 0.7); }
    .bp3-toast[class*="bp3-intent-"] a:hover{
      color:#ffffff; }
  .bp3-toast[class*="bp3-intent-"] > .bp3-icon{
    color:#ffffff; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button, .bp3-toast[class*="bp3-intent-"] .bp3-button::before,
  .bp3-toast[class*="bp3-intent-"] .bp3-button .bp3-icon, .bp3-toast[class*="bp3-intent-"] .bp3-button:active{
    color:rgba(255, 255, 255, 0.7) !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:focus{
    outline-color:rgba(255, 255, 255, 0.5); }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:hover{
    background-color:rgba(255, 255, 255, 0.15) !important;
    color:#ffffff !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:active{
    background-color:rgba(255, 255, 255, 0.3) !important;
    color:#ffffff !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button::after{
    background:rgba(255, 255, 255, 0.3) !important; }
  .bp3-toast.bp3-intent-primary{
    background-color:#137cbd;
    color:#ffffff; }
  .bp3-toast.bp3-intent-success{
    background-color:#0f9960;
    color:#ffffff; }
  .bp3-toast.bp3-intent-warning{
    background-color:#d9822b;
    color:#ffffff; }
  .bp3-toast.bp3-intent-danger{
    background-color:#db3737;
    color:#ffffff; }

.bp3-toast-message{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  padding:11px;
  word-break:break-word; }

.bp3-toast-container{
  display:-webkit-box !important;
  display:-ms-flexbox !important;
  display:flex !important;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  position:fixed;
  right:0;
  left:0;
  z-index:40;
  overflow:hidden;
  padding:0 20px 20px;
  pointer-events:none; }
  .bp3-toast-container.bp3-toast-container-top{
    top:0;
    bottom:auto; }
  .bp3-toast-container.bp3-toast-container-bottom{
    -webkit-box-orient:vertical;
    -webkit-box-direction:reverse;
        -ms-flex-direction:column-reverse;
            flex-direction:column-reverse;
    top:auto;
    bottom:0; }
  .bp3-toast-container.bp3-toast-container-left{
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start; }
  .bp3-toast-container.bp3-toast-container-right{
    -webkit-box-align:end;
        -ms-flex-align:end;
            align-items:flex-end; }

.bp3-toast-container-bottom .bp3-toast.bp3-toast-enter:not(.bp3-toast-enter-active),
.bp3-toast-container-bottom .bp3-toast.bp3-toast-enter:not(.bp3-toast-enter-active) ~ .bp3-toast, .bp3-toast-container-bottom .bp3-toast.bp3-toast-appear:not(.bp3-toast-appear-active),
.bp3-toast-container-bottom .bp3-toast.bp3-toast-appear:not(.bp3-toast-appear-active) ~ .bp3-toast,
.bp3-toast-container-bottom .bp3-toast.bp3-toast-leave-active ~ .bp3-toast{
  -webkit-transform:translateY(60px);
          transform:translateY(60px); }
.bp3-tooltip{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  -webkit-transform:scale(1);
          transform:scale(1); }
  .bp3-tooltip .bp3-popover-arrow{
    position:absolute;
    width:22px;
    height:22px; }
    .bp3-tooltip .bp3-popover-arrow::before{
      margin:4px;
      width:14px;
      height:14px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip{
    margin-top:-11px;
    margin-bottom:11px; }
    .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow{
      bottom:-8px; }
      .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(-90deg);
                transform:rotate(-90deg); }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip{
    margin-left:11px; }
    .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow{
      left:-8px; }
      .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(0);
                transform:rotate(0); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip{
    margin-top:11px; }
    .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow{
      top:-8px; }
      .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(90deg);
                transform:rotate(90deg); }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip{
    margin-right:11px;
    margin-left:-11px; }
    .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow{
      right:-8px; }
      .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(180deg);
                transform:rotate(180deg); }
  .bp3-tether-element-attached-middle > .bp3-tooltip > .bp3-popover-arrow{
    top:50%;
    -webkit-transform:translateY(-50%);
            transform:translateY(-50%); }
  .bp3-tether-element-attached-center > .bp3-tooltip > .bp3-popover-arrow{
    right:50%;
    -webkit-transform:translateX(50%);
            transform:translateX(50%); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow{
    top:-0.22183px; }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow{
    right:-0.22183px; }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow{
    left:-0.22183px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow{
    bottom:-0.22183px; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:top left;
            transform-origin:top left; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:top center;
            transform-origin:top center; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:top right;
            transform-origin:top right; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:center left;
            transform-origin:center left; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:center center;
            transform-origin:center center; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:center right;
            transform-origin:center right; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:bottom left;
            transform-origin:bottom left; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:bottom center;
            transform-origin:bottom center; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:bottom right;
            transform-origin:bottom right; }
  .bp3-tooltip .bp3-popover-content{
    background:#394b59;
    color:#f5f8fa; }
  .bp3-tooltip .bp3-popover-arrow::before{
    -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2);
            box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2); }
  .bp3-tooltip .bp3-popover-arrow-border{
    fill:#10161a;
    fill-opacity:0.1; }
  .bp3-tooltip .bp3-popover-arrow-fill{
    fill:#394b59; }
  .bp3-popover-enter > .bp3-tooltip, .bp3-popover-appear > .bp3-tooltip{
    -webkit-transform:scale(0.8);
            transform:scale(0.8); }
  .bp3-popover-enter-active > .bp3-tooltip, .bp3-popover-appear-active > .bp3-tooltip{
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-popover-exit > .bp3-tooltip{
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-popover-exit-active > .bp3-tooltip{
    -webkit-transform:scale(0.8);
            transform:scale(0.8);
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-tooltip .bp3-popover-content{
    padding:10px 12px; }
  .bp3-tooltip.bp3-dark,
  .bp3-dark .bp3-tooltip{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
    .bp3-tooltip.bp3-dark .bp3-popover-content,
    .bp3-dark .bp3-tooltip .bp3-popover-content{
      background:#e1e8ed;
      color:#394b59; }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow::before,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow::before{
      -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4);
              box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4); }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow-border,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow-border{
      fill:#10161a;
      fill-opacity:0.2; }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow-fill,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow-fill{
      fill:#e1e8ed; }
  .bp3-tooltip.bp3-intent-primary .bp3-popover-content{
    background:#137cbd;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-primary .bp3-popover-arrow-fill{
    fill:#137cbd; }
  .bp3-tooltip.bp3-intent-success .bp3-popover-content{
    background:#0f9960;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-success .bp3-popover-arrow-fill{
    fill:#0f9960; }
  .bp3-tooltip.bp3-intent-warning .bp3-popover-content{
    background:#d9822b;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-warning .bp3-popover-arrow-fill{
    fill:#d9822b; }
  .bp3-tooltip.bp3-intent-danger .bp3-popover-content{
    background:#db3737;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-danger .bp3-popover-arrow-fill{
    fill:#db3737; }

.bp3-tooltip-indicator{
  border-bottom:dotted 1px;
  cursor:help; }
.bp3-tree .bp3-icon, .bp3-tree .bp3-icon-standard, .bp3-tree .bp3-icon-large{
  color:#5c7080; }
  .bp3-tree .bp3-icon.bp3-intent-primary, .bp3-tree .bp3-icon-standard.bp3-intent-primary, .bp3-tree .bp3-icon-large.bp3-intent-primary{
    color:#137cbd; }
  .bp3-tree .bp3-icon.bp3-intent-success, .bp3-tree .bp3-icon-standard.bp3-intent-success, .bp3-tree .bp3-icon-large.bp3-intent-success{
    color:#0f9960; }
  .bp3-tree .bp3-icon.bp3-intent-warning, .bp3-tree .bp3-icon-standard.bp3-intent-warning, .bp3-tree .bp3-icon-large.bp3-intent-warning{
    color:#d9822b; }
  .bp3-tree .bp3-icon.bp3-intent-danger, .bp3-tree .bp3-icon-standard.bp3-intent-danger, .bp3-tree .bp3-icon-large.bp3-intent-danger{
    color:#db3737; }

.bp3-tree-node-list{
  margin:0;
  padding-left:0;
  list-style:none; }

.bp3-tree-root{
  position:relative;
  background-color:transparent;
  cursor:default;
  padding-left:0; }

.bp3-tree-node-content-0{
  padding-left:0px; }

.bp3-tree-node-content-1{
  padding-left:23px; }

.bp3-tree-node-content-2{
  padding-left:46px; }

.bp3-tree-node-content-3{
  padding-left:69px; }

.bp3-tree-node-content-4{
  padding-left:92px; }

.bp3-tree-node-content-5{
  padding-left:115px; }

.bp3-tree-node-content-6{
  padding-left:138px; }

.bp3-tree-node-content-7{
  padding-left:161px; }

.bp3-tree-node-content-8{
  padding-left:184px; }

.bp3-tree-node-content-9{
  padding-left:207px; }

.bp3-tree-node-content-10{
  padding-left:230px; }

.bp3-tree-node-content-11{
  padding-left:253px; }

.bp3-tree-node-content-12{
  padding-left:276px; }

.bp3-tree-node-content-13{
  padding-left:299px; }

.bp3-tree-node-content-14{
  padding-left:322px; }

.bp3-tree-node-content-15{
  padding-left:345px; }

.bp3-tree-node-content-16{
  padding-left:368px; }

.bp3-tree-node-content-17{
  padding-left:391px; }

.bp3-tree-node-content-18{
  padding-left:414px; }

.bp3-tree-node-content-19{
  padding-left:437px; }

.bp3-tree-node-content-20{
  padding-left:460px; }

.bp3-tree-node-content{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  width:100%;
  height:30px;
  padding-right:5px; }
  .bp3-tree-node-content:hover{
    background-color:rgba(191, 204, 214, 0.4); }

.bp3-tree-node-caret,
.bp3-tree-node-caret-none{
  min-width:30px; }

.bp3-tree-node-caret{
  color:#5c7080;
  -webkit-transform:rotate(0deg);
          transform:rotate(0deg);
  cursor:pointer;
  padding:7px;
  -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-tree-node-caret:hover{
    color:#182026; }
  .bp3-dark .bp3-tree-node-caret{
    color:#a7b6c2; }
    .bp3-dark .bp3-tree-node-caret:hover{
      color:#f5f8fa; }
  .bp3-tree-node-caret.bp3-tree-node-caret-open{
    -webkit-transform:rotate(90deg);
            transform:rotate(90deg); }
  .bp3-tree-node-caret.bp3-icon-standard::before{
    content:""; }

.bp3-tree-node-icon{
  position:relative;
  margin-right:7px; }

.bp3-tree-node-label{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  position:relative;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-tree-node-label span{
    display:inline; }

.bp3-tree-node-secondary-label{
  padding:0 5px;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-tree-node-secondary-label .bp3-popover-wrapper,
  .bp3-tree-node-secondary-label .bp3-popover-target{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center; }

.bp3-tree-node.bp3-disabled .bp3-tree-node-content{
  background-color:inherit;
  cursor:not-allowed;
  color:rgba(92, 112, 128, 0.6); }

.bp3-tree-node.bp3-disabled .bp3-tree-node-caret,
.bp3-tree-node.bp3-disabled .bp3-tree-node-icon{
  cursor:not-allowed;
  color:rgba(92, 112, 128, 0.6); }

.bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content{
  background-color:#137cbd; }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content,
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon, .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon-standard, .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon-large{
    color:#ffffff; }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-tree-node-caret::before{
    color:rgba(255, 255, 255, 0.7); }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-tree-node-caret:hover::before{
    color:#ffffff; }

.bp3-dark .bp3-tree-node-content:hover{
  background-color:rgba(92, 112, 128, 0.3); }

.bp3-dark .bp3-tree .bp3-icon, .bp3-dark .bp3-tree .bp3-icon-standard, .bp3-dark .bp3-tree .bp3-icon-large{
  color:#a7b6c2; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-primary, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-primary, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-primary{
    color:#137cbd; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-success, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-success, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-success{
    color:#0f9960; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-warning, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-warning, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-warning{
    color:#d9822b; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-danger, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-danger, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-danger{
    color:#db3737; }

.bp3-dark .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content{
  background-color:#137cbd; }
/*!

Copyright 2017-present Palantir Technologies, Inc. All rights reserved.
Licensed under the Apache License, Version 2.0.

*/
.bp3-omnibar{
  -webkit-filter:blur(0);
          filter:blur(0);
  opacity:1;
  top:20vh;
  left:calc(50% - 250px);
  z-index:21;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  background-color:#ffffff;
  width:500px; }
  .bp3-omnibar.bp3-overlay-enter, .bp3-omnibar.bp3-overlay-appear{
    -webkit-filter:blur(20px);
            filter:blur(20px);
    opacity:0.2; }
  .bp3-omnibar.bp3-overlay-enter-active, .bp3-omnibar.bp3-overlay-appear-active{
    -webkit-filter:blur(0);
            filter:blur(0);
    opacity:1;
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:filter, opacity;
    transition-property:filter, opacity, -webkit-filter;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-omnibar.bp3-overlay-exit{
    -webkit-filter:blur(0);
            filter:blur(0);
    opacity:1; }
  .bp3-omnibar.bp3-overlay-exit-active{
    -webkit-filter:blur(20px);
            filter:blur(20px);
    opacity:0.2;
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:filter, opacity;
    transition-property:filter, opacity, -webkit-filter;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
    -webkit-transition-delay:0;
            transition-delay:0; }
  .bp3-omnibar .bp3-input{
    border-radius:0;
    background-color:transparent; }
    .bp3-omnibar .bp3-input, .bp3-omnibar .bp3-input:focus{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-omnibar .bp3-menu{
    border-radius:0;
    -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
    background-color:transparent;
    max-height:calc(60vh - 40px);
    overflow:auto; }
    .bp3-omnibar .bp3-menu:empty{
      display:none; }
  .bp3-dark .bp3-omnibar, .bp3-omnibar.bp3-dark{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
    background-color:#30404d; }

.bp3-omnibar-overlay .bp3-overlay-backdrop{
  background-color:rgba(16, 22, 26, 0.2); }

.bp3-select-popover .bp3-popover-content{
  padding:5px; }

.bp3-select-popover .bp3-input-group{
  margin-bottom:0; }

.bp3-select-popover .bp3-menu{
  max-width:400px;
  max-height:300px;
  overflow:auto;
  padding:0; }
  .bp3-select-popover .bp3-menu:not(:first-child){
    padding-top:5px; }

.bp3-multi-select{
  min-width:150px; }

.bp3-multi-select-popover .bp3-menu{
  max-width:400px;
  max-height:300px;
  overflow:auto; }

.bp3-select-popover .bp3-popover-content{
  padding:5px; }

.bp3-select-popover .bp3-input-group{
  margin-bottom:0; }

.bp3-select-popover .bp3-menu{
  max-width:400px;
  max-height:300px;
  overflow:auto;
  padding:0; }
  .bp3-select-popover .bp3-menu:not(:first-child){
    padding-top:5px; }
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDhoLTIuODFjLS40NS0uNzgtMS4wNy0xLjQ1LTEuODItMS45NkwxNyA0LjQxIDE1LjU5IDNsLTIuMTcgMi4xN0MxMi45NiA1LjA2IDEyLjQ5IDUgMTIgNWMtLjQ5IDAtLjk2LjA2LTEuNDEuMTdMOC40MSAzIDcgNC40MWwxLjYyIDEuNjNDNy44OCA2LjU1IDcuMjYgNy4yMiA2LjgxIDhINHYyaDIuMDljLS4wNS4zMy0uMDkuNjYtLjA5IDF2MUg0djJoMnYxYzAgLjM0LjA0LjY3LjA5IDFINHYyaDIuODFjMS4wNCAxLjc5IDIuOTcgMyA1LjE5IDNzNC4xNS0xLjIxIDUuMTktM0gyMHYtMmgtMi4wOWMuMDUtLjMzLjA5LS42Ni4wOS0xdi0xaDJ2LTJoLTJ2LTFjMC0uMzQtLjA0LS42Ny0uMDktMUgyMFY4em0tNiA4aC00di0yaDR2MnptMC00aC00di0yaDR2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTYuMTdMNC44MyAxMmwtMS40MiAxLjQxTDkgMTkgMjEgN2wtMS40MS0xLjQxeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1pY29uLWJyYW5kMSBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNmZmYiPgogICAgPHBhdGggZD0iTTEwNSAxMjcuM2g0MHYxMi44aC00MHpNNTEuMSA3N0w3NCA5OS45bC0yMy4zIDIzLjMgMTAuNSAxMC41IDIzLjMtMjMuM0w5NSA5OS45IDg0LjUgODkuNCA2MS42IDY2LjV6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMSBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNGOUE4MjUiPgogICAgPHBhdGggZD0iTTIwLjIgMTEuOGMtMS42IDAtMS43LjUtMS43IDEgMCAuNC4xLjkuMSAxLjMuMS41LjEuOS4xIDEuMyAwIDEuNy0xLjQgMi4zLTMuNSAyLjNoLS45di0xLjloLjVjMS4xIDAgMS40IDAgMS40LS44IDAtLjMgMC0uNi0uMS0xIDAtLjQtLjEtLjgtLjEtMS4yIDAtMS4zIDAtMS44IDEuMy0yLTEuMy0uMi0xLjMtLjctMS4zLTIgMC0uNC4xLS44LjEtMS4yLjEtLjQuMS0uNy4xLTEgMC0uOC0uNC0uNy0xLjQtLjhoLS41VjQuMWguOWMyLjIgMCAzLjUuNyAzLjUgMi4zIDAgLjQtLjEuOS0uMSAxLjMtLjEuNS0uMS45LS4xIDEuMyAwIC41LjIgMSAxLjcgMXYxLjh6TTEuOCAxMC4xYzEuNiAwIDEuNy0uNSAxLjctMSAwLS40LS4xLS45LS4xLTEuMy0uMS0uNS0uMS0uOS0uMS0xLjMgMC0xLjYgMS40LTIuMyAzLjUtMi4zaC45djEuOWgtLjVjLTEgMC0xLjQgMC0xLjQuOCAwIC4zIDAgLjYuMSAxIDAgLjIuMS42LjEgMSAwIDEuMyAwIDEuOC0xLjMgMkM2IDExLjIgNiAxMS43IDYgMTNjMCAuNC0uMS44LS4xIDEuMi0uMS4zLS4xLjctLjEgMSAwIC44LjMuOCAxLjQuOGguNXYxLjloLS45Yy0yLjEgMC0zLjUtLjYtMy41LTIuMyAwLS40LjEtLjkuMS0xLjMuMS0uNS4xLS45LjEtMS4zIDAtLjUtLjItMS0xLjctMXYtMS45eiIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSIxMy44IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY3g9IjExIiBjeT0iOC4yIiByPSIyLjEiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgPGcgY2xhc3M9ImpwLWljb24td2FybjAiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4=);
  --jp-icon-listings-info: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pg0KPHN2ZyB2ZXJzaW9uPSIxLjEiIGlkPSJDYXBhXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4Ig0KCSB2aWV3Qm94PSIwIDAgNTAuOTc4IDUwLjk3OCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgNTAuOTc4IDUwLjk3ODsiIHhtbDpzcGFjZT0icHJlc2VydmUiPg0KPGc+DQoJPGc+DQoJCTxnPg0KCQkJPHBhdGggc3R5bGU9ImZpbGw6IzAxMDAwMjsiIGQ9Ik00My41Miw3LjQ1OEMzOC43MTEsMi42NDgsMzIuMzA3LDAsMjUuNDg5LDBDMTguNjcsMCwxMi4yNjYsMi42NDgsNy40NTgsNy40NTgNCgkJCQljLTkuOTQzLDkuOTQxLTkuOTQzLDI2LjExOSwwLDM2LjA2MmM0LjgwOSw0LjgwOSwxMS4yMTIsNy40NTYsMTguMDMxLDcuNDU4YzAsMCwwLjAwMSwwLDAuMDAyLDANCgkJCQljNi44MTYsMCwxMy4yMjEtMi42NDgsMTguMDI5LTcuNDU4YzQuODA5LTQuODA5LDcuNDU3LTExLjIxMiw3LjQ1Ny0xOC4wM0M1MC45NzcsMTguNjcsNDguMzI4LDEyLjI2Niw0My41Miw3LjQ1OHoNCgkJCQkgTTQyLjEwNiw0Mi4xMDVjLTQuNDMyLDQuNDMxLTEwLjMzMiw2Ljg3Mi0xNi42MTUsNi44NzJoLTAuMDAyYy02LjI4NS0wLjAwMS0xMi4xODctMi40NDEtMTYuNjE3LTYuODcyDQoJCQkJYy05LjE2Mi05LjE2My05LjE2Mi0yNC4wNzEsMC0zMy4yMzNDMTMuMzAzLDQuNDQsMTkuMjA0LDIsMjUuNDg5LDJjNi4yODQsMCwxMi4xODYsMi40NCwxNi42MTcsNi44NzINCgkJCQljNC40MzEsNC40MzEsNi44NzEsMTAuMzMyLDYuODcxLDE2LjYxN0M0OC45NzcsMzEuNzcyLDQ2LjUzNiwzNy42NzUsNDIuMTA2LDQyLjEwNXoiLz4NCgkJPC9nPg0KCQk8Zz4NCgkJCTxwYXRoIHN0eWxlPSJmaWxsOiMwMTAwMDI7IiBkPSJNMjMuNTc4LDMyLjIxOGMtMC4wMjMtMS43MzQsMC4xNDMtMy4wNTksMC40OTYtMy45NzJjMC4zNTMtMC45MTMsMS4xMS0xLjk5NywyLjI3Mi0zLjI1Mw0KCQkJCWMwLjQ2OC0wLjUzNiwwLjkyMy0xLjA2MiwxLjM2Ny0xLjU3NWMwLjYyNi0wLjc1MywxLjEwNC0xLjQ3OCwxLjQzNi0yLjE3NWMwLjMzMS0wLjcwNywwLjQ5NS0xLjU0MSwwLjQ5NS0yLjUNCgkJCQljMC0xLjA5Ni0wLjI2LTIuMDg4LTAuNzc5LTIuOTc5Yy0wLjU2NS0wLjg3OS0xLjUwMS0xLjMzNi0yLjgwNi0xLjM2OWMtMS44MDIsMC4wNTctMi45ODUsMC42NjctMy41NSwxLjgzMg0KCQkJCWMtMC4zMDEsMC41MzUtMC41MDMsMS4xNDEtMC42MDcsMS44MTRjLTAuMTM5LDAuNzA3LTAuMjA3LDEuNDMyLTAuMjA3LDIuMTc0aC0yLjkzN2MtMC4wOTEtMi4yMDgsMC40MDctNC4xMTQsMS40OTMtNS43MTkNCgkJCQljMS4wNjItMS42NCwyLjg1NS0yLjQ4MSw1LjM3OC0yLjUyN2MyLjE2LDAuMDIzLDMuODc0LDAuNjA4LDUuMTQxLDEuNzU4YzEuMjc4LDEuMTYsMS45MjksMi43NjQsMS45NSw0LjgxMQ0KCQkJCWMwLDEuMTQyLTAuMTM3LDIuMTExLTAuNDEsMi45MTFjLTAuMzA5LDAuODQ1LTAuNzMxLDEuNTkzLTEuMjY4LDIuMjQzYy0wLjQ5MiwwLjY1LTEuMDY4LDEuMzE4LTEuNzMsMi4wMDINCgkJCQljLTAuNjUsMC42OTctMS4zMTMsMS40NzktMS45ODcsMi4zNDZjLTAuMjM5LDAuMzc3LTAuNDI5LDAuNzc3LTAuNTY1LDEuMTk5Yy0wLjE2LDAuOTU5LTAuMjE3LDEuOTUxLTAuMTcxLDIuOTc5DQoJCQkJQzI2LjU4OSwzMi4yMTgsMjMuNTc4LDMyLjIxOCwyMy41NzgsMzIuMjE4eiBNMjMuNTc4LDM4LjIydi0zLjQ4NGgzLjA3NnYzLjQ4NEgyMy41Nzh6Ii8+DQoJCTwvZz4NCgk8L2c+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8L3N2Zz4NCg==);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMEQ0N0ExIj4KICAgIDxwYXRoIGQ9Ik0xMS4xIDYuOVY1LjhINi45YzAtLjUgMC0xLjMuMi0xLjYuNC0uNy44LTEuMSAxLjctMS40IDEuNy0uMyAyLjUtLjMgMy45LS4xIDEgLjEgMS45LjkgMS45IDEuOXY0LjJjMCAuNS0uOSAxLjYtMiAxLjZIOC44Yy0xLjUgMC0yLjQgMS40LTIuNCAyLjh2Mi4ySDQuN0MzLjUgMTUuMSAzIDE0IDMgMTMuMVY5Yy0uMS0xIC42LTIgMS44LTIgMS41LS4xIDYuMy0uMSA2LjMtLjF6Ii8+CiAgICA8cGF0aCBkPSJNMTAuOSAxNS4xdjEuMWg0LjJjMCAuNSAwIDEuMy0uMiAxLjYtLjQuNy0uOCAxLjEtMS43IDEuNC0xLjcuMy0yLjUuMy0zLjkuMS0xLS4xLTEuOS0uOS0xLjktMS45di00LjJjMC0uNS45LTEuNiAyLTEuNmgzLjhjMS41IDAgMi40LTEuNCAyLjQtMi44VjYuNmgxLjdDMTguNSA2LjkgMTkgOCAxOSA4LjlWMTNjMCAxLS43IDIuMS0xLjkgMi4xaC02LjJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiB3aWR0aD0iMjAiIGhlaWdodD0iMjAiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMikiIGZpbGw9IiMzMzMzMzMiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uLWFjY2VudDIganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGQ9Ik01LjA1NjY0IDguNzYxNzJDNS4wNTY2NCA4LjU5NzY2IDUuMDMxMjUgOC40NTMxMiA0Ljk4MDQ3IDguMzI4MTJDNC45MzM1OSA4LjE5OTIyIDQuODU1NDcgOC4wODIwMyA0Ljc0NjA5IDcuOTc2NTZDNC42NDA2MiA3Ljg3MTA5IDQuNSA3Ljc3NTM5IDQuMzI0MjIgNy42ODk0NUM0LjE1MjM0IDcuNTk5NjEgMy45NDMzNiA3LjUxMTcyIDMuNjk3MjcgNy40MjU3OEMzLjMwMjczIDcuMjg1MTYgMi45NDMzNiA3LjEzNjcyIDIuNjE5MTQgNi45ODA0N0MyLjI5NDkyIDYuODI0MjIgMi4wMTc1OCA2LjY0MjU4IDEuNzg3MTEgNi40MzU1NUMxLjU2MDU1IDYuMjI4NTIgMS4zODQ3NyA1Ljk4ODI4IDEuMjU5NzcgNS43MTQ4NEMxLjEzNDc3IDUuNDM3NSAxLjA3MjI3IDUuMTA5MzggMS4wNzIyNyA0LjczMDQ3QzEuMDcyMjcgNC4zOTg0NCAxLjEyODkxIDQuMDk1NyAxLjI0MjE5IDMuODIyMjdDMS4zNTU0NyAzLjU0NDkyIDEuNTE1NjIgMy4zMDQ2OSAxLjcyMjY2IDMuMTAxNTZDMS45Mjk2OSAyLjg5ODQ0IDIuMTc5NjkgMi43MzQzNyAyLjQ3MjY2IDIuNjA5MzhDMi43NjU2MiAyLjQ4NDM4IDMuMDkxOCAyLjQwNDMgMy40NTExNyAyLjM2OTE0VjEuMTA5MzhINC4zODg2N1YyLjM4MDg2QzQuNzQwMjMgMi40Mjc3MyA1LjA1NjY0IDIuNTIzNDQgNS4zMzc4OSAyLjY2Nzk3QzUuNjE5MTQgMi44MTI1IDUuODU3NDIgMy4wMDE5NSA2LjA1MjczIDMuMjM2MzNDNi4yNTE5NSAzLjQ2NjggNi40MDQzIDMuNzQwMjMgNi41MDk3NyA0LjA1NjY0QzYuNjE5MTQgNC4zNjkxNCA2LjY3MzgzIDQuNzIwNyA2LjY3MzgzIDUuMTExMzNINS4wNDQ5MkM1LjA0NDkyIDQuNjM4NjcgNC45Mzc1IDQuMjgxMjUgNC43MjI2NiA0LjAzOTA2QzQuNTA3ODEgMy43OTI5NyA0LjIxNjggMy42Njk5MiAzLjg0OTYxIDMuNjY5OTJDMy42NTAzOSAzLjY2OTkyIDMuNDc2NTYgMy42OTcyNyAzLjMyODEyIDMuNzUxOTVDMy4xODM1OSAzLjgwMjczIDMuMDY0NDUgMy44NzY5NSAyLjk3MDcgMy45NzQ2MUMyLjg3Njk1IDQuMDY4MzYgMi44MDY2NCA0LjE3OTY5IDIuNzU5NzcgNC4zMDg1OUMyLjcxNjggNC40Mzc1IDIuNjk1MzEgNC41NzgxMiAyLjY5NTMxIDQuNzMwNDdDMi42OTUzMSA0Ljg4MjgxIDIuNzE2OCA1LjAxOTUzIDIuNzU5NzcgNS4xNDA2MkMyLjgwNjY0IDUuMjU3ODEgMi44ODI4MSA1LjM2NzE5IDIuOTg4MjggNS40Njg3NUMzLjA5NzY2IDUuNTcwMzEgMy4yNDAyMyA1LjY2Nzk3IDMuNDE2MDIgNS43NjE3MkMzLjU5MTggNS44NTE1NiAzLjgxMDU1IDUuOTQzMzYgNC4wNzIyNyA2LjAzNzExQzQuNDY2OCA2LjE4NTU1IDQuODI0MjIgNi4zMzk4NCA1LjE0NDUzIDYuNUM1LjQ2NDg0IDYuNjU2MjUgNS43MzgyOCA2LjgzOTg0IDUuOTY0ODQgNy4wNTA3OEM2LjE5NTMxIDcuMjU3ODEgNi4zNzEwOSA3LjUgNi40OTIxOSA3Ljc3NzM0QzYuNjE3MTkgOC4wNTA3OCA2LjY3OTY5IDguMzc1IDYuNjc5NjkgOC43NUM2LjY3OTY5IDkuMDkzNzUgNi42MjMwNSA5LjQwNDMgNi41MDk3NyA5LjY4MTY0QzYuMzk2NDggOS45NTUwOCA2LjIzNDM4IDEwLjE5MTQgNi4wMjM0NCAxMC4zOTA2QzUuODEyNSAxMC41ODk4IDUuNTU4NTkgMTAuNzUgNS4yNjE3MiAxMC44NzExQzQuOTY0ODQgMTAuOTg4MyA0LjYzMjgxIDExLjA2NDUgNC4yNjU2MiAxMS4wOTk2VjEyLjI0OEgzLjMzMzk4VjExLjA5OTZDMy4wMDE5NSAxMS4wNjg0IDIuNjc5NjkgMTAuOTk2MSAyLjM2NzE5IDEwLjg4MjhDMi4wNTQ2OSAxMC43NjU2IDEuNzc3MzQgMTAuNTk3NyAxLjUzNTE2IDEwLjM3ODlDMS4yOTY4OCAxMC4xNjAyIDEuMTA1NDcgOS44ODQ3NyAwLjk2MDkzOCA5LjU1MjczQzAuODE2NDA2IDkuMjE2OCAwLjc0NDE0MSA4LjgxNDQ1IDAuNzQ0MTQxIDguMzQ1N0gyLjM3ODkxQzIuMzc4OTEgOC42MjY5NSAyLjQxOTkyIDguODYzMjggMi41MDE5NSA5LjA1NDY5QzIuNTgzOTggOS4yNDIxOSAyLjY4OTQ1IDkuMzkyNTggMi44MTgzNiA5LjUwNTg2QzIuOTUxMTcgOS42MTUyMyAzLjEwMTU2IDkuNjkzMzYgMy4yNjk1MyA5Ljc0MDIzQzMuNDM3NSA5Ljc4NzExIDMuNjA5MzggOS44MTA1NSAzLjc4NTE2IDkuODEwNTVDNC4yMDMxMiA5LjgxMDU1IDQuNTE5NTMgOS43MTI4OSA0LjczNDM4IDkuNTE3NThDNC45NDkyMiA5LjMyMjI3IDUuMDU2NjQgOS4wNzAzMSA1LjA1NjY0IDguNzYxNzJaTTEzLjQxOCAxMi4yNzE1SDguMDc0MjJWMTFIMTMuNDE4VjEyLjI3MTVaIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzLjk1MjY0IDYpIiBmaWxsPSJ3aGl0ZSIvPgo8L3N2Zz4K);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTUgMTVIM3YyaDEydi0yem0wLThIM3YyaDEyVjd6TTMgMTNoMTh2LTJIM3Yyem0wIDhoMTh2LTJIM3Yyek0zIDN2MmgxOFYzSDN6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}
.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}
.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}
.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}
.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}
.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}
.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}
.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}
.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}
.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}
.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}
.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}
.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}
.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}
.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}
.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}
.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}
.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}
.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}
.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}
.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}
.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}
.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}
.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}
.jp-FileIcon {
  background-image: var(--jp-icon-file);
}
.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}
.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}
.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}
.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}
.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}
.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}
.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}
.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}
.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}
.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}
.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}
.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}
.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}
.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}
.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}
.jp-ListIcon {
  background-image: var(--jp-icon-list);
}
.jp-ListingsInfoIcon {
  background-image: var(--jp-icon-listings-info);
}
.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}
.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}
.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}
.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}
.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}
.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}
.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}
.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}
.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}
.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}
.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}
.jp-RunIcon {
  background-image: var(--jp-icon-run);
}
.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}
.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}
.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}
.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}
.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}
.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}
.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}
.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}
.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}
.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}
.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}
.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}
.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

:root {
  --jp-icon-search-white: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
}

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}
/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}
/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}
/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}
.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}
.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}
.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}
.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}
.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}
.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}
.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}
.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}
/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}
.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}
.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}
.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}
.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}
.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}
.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}
/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}
.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}
.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}
.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}
.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}
.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}
.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

/* CSS for icons in selected items in the settings editor */
#setting-editor .jp-PluginList .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}
#setting-editor
  .jp-PluginList
  .jp-mod-selected
  .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* CSS for icons in selected tabs in the sidebar tab manager */
#tab-manager .lm-TabBar-tab.jp-mod-active .jp-icon-selectable[fill] {
  fill: #fff;
}

#tab-manager .lm-TabBar-tab.jp-mod-active .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}
#tab-manager
  .lm-TabBar-tab.jp-mod-active
  .jp-icon-hover
  :hover
  .jp-icon-selectable[fill] {
  fill: var(--jp-brand-color1);
}

#tab-manager
  .lm-TabBar-tab.jp-mod-active
  .jp-icon-hover
  :hover
  .jp-icon-selectable-inverse[fill] {
  fill: #fff;
}

/**
 * TODO: come up with non css-hack solution for showing the busy icon on top
 *  of the close icon
 * CSS for complex behavior of close icon of tabs in the sidebar tab manager
 */
#tab-manager
  .lm-TabBar-tab.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}
#tab-manager
  .lm-TabBar-tab.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

#tab-manager
  .lm-TabBar-tab.jp-mod-dirty.jp-mod-active
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: #fff;
}

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}
/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) svg {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

/* Override Blueprint's _reset.scss styles */
html {
  box-sizing: unset;
}

*,
*::before,
*::after {
  box-sizing: unset;
}

body {
  color: unset;
  font-family: var(--jp-ui-font-family);
}

p {
  margin-top: unset;
  margin-bottom: unset;
}

small {
  font-size: unset;
}

strong {
  font-weight: unset;
}

/* Override Blueprint's _typography.scss styles */
a {
  text-decoration: unset;
  color: unset;
}
a:hover {
  text-decoration: unset;
  color: unset;
}

/* Override Blueprint's _accessibility.scss styles */
:focus {
  outline: unset;
  outline-offset: unset;
  -moz-outline-radius: unset;
}

/* Styles for ui-components */
.jp-Button {
  border-radius: var(--jp-border-radius);
  padding: 0px 12px;
  font-size: var(--jp-ui-font-size1);
}

/* Use our own theme for hover styles */
button.jp-Button.bp3-button.bp3-minimal:hover {
  background-color: var(--jp-layout-color2);
}
.jp-Button.minimal {
  color: unset !important;
}

.jp-Button.jp-ToolbarButtonComponent {
  text-transform: none;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color3);
}

.jp-BPIcon {
  display: inline-block;
  vertical-align: middle;
  margin: auto;
}

/* Stop blueprint futzing with our icon fills */
.bp3-icon.jp-BPIcon > svg:not([fill]) {
  fill: var(--jp-inverse-layout-color3);
}

.jp-InputGroupAction {
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

/* Use our own theme for hover and option styles */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}
select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-top: 1px solid var(--jp-border-color2);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-Collapse-header {
  padding: 1px 12px;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size2);
}

.jp-Collapse-header:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Collapse-contents {
  padding: 0px 12px 0px 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0px;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0px 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.lm-CommandPalette-wrapper::after {
  content: ' ';
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  height: 30px;
  width: 10px;
  padding: 0px 10px;
  background-image: var(--jp-icon-search-white);
  background-size: 20px;
  background-repeat: no-repeat;
  background-position: center;
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color3);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0px;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color3);
}

.lm-CommandPalette-item.lm-mod-active {
  background: var(--jp-layout-color3);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  background: var(--jp-layout-color4);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color3);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.4;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty:after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0px 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0px;
  left: 0px;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px;
  padding-bottom: 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0px;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

.jp-Dialog-header {
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0px 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

.jp-HoverBox.jp-mod-outofview {
  display: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `p-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;

  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;

  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #aa00ff;

  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;

  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;

  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;

  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;

  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;

  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;

  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;

  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;

  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;

  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ffff00;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;

  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;

  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;

  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;

  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;

  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eeeeee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;

  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent:before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent:after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0px 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  height: 28px;
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  background-color: var(--jp-layout-color1);
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0px 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  height: 32px;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 1;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0px;
  margin: 0px;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0px 6px;
  margin: 0px;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent span {
  padding: 0px;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ body.p-mod-override-cursor *, /* </DEPRECATED> */
body.lm-mod-override-cursor * {
  cursor: inherit !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0px;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* BASICS */

.CodeMirror {
  /* Set height, width, borders, and global font properties here */
  font-family: monospace;
  height: 300px;
  color: black;
  direction: ltr;
}

/* PADDING */

.CodeMirror-lines {
  padding: 4px 0; /* Vertical padding around content */
}
.CodeMirror pre.CodeMirror-line,
.CodeMirror pre.CodeMirror-line-like {
  padding: 0 4px; /* Horizontal padding of content */
}

.CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler {
  background-color: white; /* The little square between H and V scrollbars */
}

/* GUTTER */

.CodeMirror-gutters {
  border-right: 1px solid #ddd;
  background-color: #f7f7f7;
  white-space: nowrap;
}
.CodeMirror-linenumbers {}
.CodeMirror-linenumber {
  padding: 0 3px 0 5px;
  min-width: 20px;
  text-align: right;
  color: #999;
  white-space: nowrap;
}

.CodeMirror-guttermarker { color: black; }
.CodeMirror-guttermarker-subtle { color: #999; }

/* CURSOR */

.CodeMirror-cursor {
  border-left: 1px solid black;
  border-right: none;
  width: 0;
}
/* Shown when moving in bi-directional text */
.CodeMirror div.CodeMirror-secondarycursor {
  border-left: 1px solid silver;
}
.cm-fat-cursor .CodeMirror-cursor {
  width: auto;
  border: 0 !important;
  background: #7e7;
}
.cm-fat-cursor div.CodeMirror-cursors {
  z-index: 1;
}
.cm-fat-cursor-mark {
  background-color: rgba(20, 255, 20, 0.5);
  -webkit-animation: blink 1.06s steps(1) infinite;
  -moz-animation: blink 1.06s steps(1) infinite;
  animation: blink 1.06s steps(1) infinite;
}
.cm-animate-fat-cursor {
  width: auto;
  border: 0;
  -webkit-animation: blink 1.06s steps(1) infinite;
  -moz-animation: blink 1.06s steps(1) infinite;
  animation: blink 1.06s steps(1) infinite;
  background-color: #7e7;
}
@-moz-keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}
@-webkit-keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}
@keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}

/* Can style cursor different in overwrite (non-insert) mode */
.CodeMirror-overwrite .CodeMirror-cursor {}

.cm-tab { display: inline-block; text-decoration: inherit; }

.CodeMirror-rulers {
  position: absolute;
  left: 0; right: 0; top: -50px; bottom: 0;
  overflow: hidden;
}
.CodeMirror-ruler {
  border-left: 1px solid #ccc;
  top: 0; bottom: 0;
  position: absolute;
}

/* DEFAULT THEME */

.cm-s-default .cm-header {color: blue;}
.cm-s-default .cm-quote {color: #090;}
.cm-negative {color: #d44;}
.cm-positive {color: #292;}
.cm-header, .cm-strong {font-weight: bold;}
.cm-em {font-style: italic;}
.cm-link {text-decoration: underline;}
.cm-strikethrough {text-decoration: line-through;}

.cm-s-default .cm-keyword {color: #708;}
.cm-s-default .cm-atom {color: #219;}
.cm-s-default .cm-number {color: #164;}
.cm-s-default .cm-def {color: #00f;}
.cm-s-default .cm-variable,
.cm-s-default .cm-punctuation,
.cm-s-default .cm-property,
.cm-s-default .cm-operator {}
.cm-s-default .cm-variable-2 {color: #05a;}
.cm-s-default .cm-variable-3, .cm-s-default .cm-type {color: #085;}
.cm-s-default .cm-comment {color: #a50;}
.cm-s-default .cm-string {color: #a11;}
.cm-s-default .cm-string-2 {color: #f50;}
.cm-s-default .cm-meta {color: #555;}
.cm-s-default .cm-qualifier {color: #555;}
.cm-s-default .cm-builtin {color: #30a;}
.cm-s-default .cm-bracket {color: #997;}
.cm-s-default .cm-tag {color: #170;}
.cm-s-default .cm-attribute {color: #00c;}
.cm-s-default .cm-hr {color: #999;}
.cm-s-default .cm-link {color: #00c;}

.cm-s-default .cm-error {color: #f00;}
.cm-invalidchar {color: #f00;}

.CodeMirror-composing { border-bottom: 2px solid; }

/* Default styles for common addons */

div.CodeMirror span.CodeMirror-matchingbracket {color: #0b0;}
div.CodeMirror span.CodeMirror-nonmatchingbracket {color: #a22;}
.CodeMirror-matchingtag { background: rgba(255, 150, 0, .3); }
.CodeMirror-activeline-background {background: #e8f2ff;}

/* STOP */

/* The rest of this file contains styles related to the mechanics of
   the editor. You probably shouldn't touch them. */

.CodeMirror {
  position: relative;
  overflow: hidden;
  background: white;
}

.CodeMirror-scroll {
  overflow: scroll !important; /* Things will break if this is overridden */
  /* 30px is the magic margin used to hide the element's real scrollbars */
  /* See overflow: hidden in .CodeMirror */
  margin-bottom: -30px; margin-right: -30px;
  padding-bottom: 30px;
  height: 100%;
  outline: none; /* Prevent dragging from highlighting the element */
  position: relative;
}
.CodeMirror-sizer {
  position: relative;
  border-right: 30px solid transparent;
}

/* The fake, visible scrollbars. Used to force redraw during scrolling
   before actual scrolling happens, thus preventing shaking and
   flickering artifacts. */
.CodeMirror-vscrollbar, .CodeMirror-hscrollbar, .CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler {
  position: absolute;
  z-index: 6;
  display: none;
}
.CodeMirror-vscrollbar {
  right: 0; top: 0;
  overflow-x: hidden;
  overflow-y: scroll;
}
.CodeMirror-hscrollbar {
  bottom: 0; left: 0;
  overflow-y: hidden;
  overflow-x: scroll;
}
.CodeMirror-scrollbar-filler {
  right: 0; bottom: 0;
}
.CodeMirror-gutter-filler {
  left: 0; bottom: 0;
}

.CodeMirror-gutters {
  position: absolute; left: 0; top: 0;
  min-height: 100%;
  z-index: 3;
}
.CodeMirror-gutter {
  white-space: normal;
  height: 100%;
  display: inline-block;
  vertical-align: top;
  margin-bottom: -30px;
}
.CodeMirror-gutter-wrapper {
  position: absolute;
  z-index: 4;
  background: none !important;
  border: none !important;
}
.CodeMirror-gutter-background {
  position: absolute;
  top: 0; bottom: 0;
  z-index: 4;
}
.CodeMirror-gutter-elt {
  position: absolute;
  cursor: default;
  z-index: 4;
}
.CodeMirror-gutter-wrapper ::selection { background-color: transparent }
.CodeMirror-gutter-wrapper ::-moz-selection { background-color: transparent }

.CodeMirror-lines {
  cursor: text;
  min-height: 1px; /* prevents collapsing before first draw */
}
.CodeMirror pre.CodeMirror-line,
.CodeMirror pre.CodeMirror-line-like {
  /* Reset some styles that the rest of the page might have set */
  -moz-border-radius: 0; -webkit-border-radius: 0; border-radius: 0;
  border-width: 0;
  background: transparent;
  font-family: inherit;
  font-size: inherit;
  margin: 0;
  white-space: pre;
  word-wrap: normal;
  line-height: inherit;
  color: inherit;
  z-index: 2;
  position: relative;
  overflow: visible;
  -webkit-tap-highlight-color: transparent;
  -webkit-font-variant-ligatures: contextual;
  font-variant-ligatures: contextual;
}
.CodeMirror-wrap pre.CodeMirror-line,
.CodeMirror-wrap pre.CodeMirror-line-like {
  word-wrap: break-word;
  white-space: pre-wrap;
  word-break: normal;
}

.CodeMirror-linebackground {
  position: absolute;
  left: 0; right: 0; top: 0; bottom: 0;
  z-index: 0;
}

.CodeMirror-linewidget {
  position: relative;
  z-index: 2;
  padding: 0.1px; /* Force widget margins to stay inside of the container */
}

.CodeMirror-widget {}

.CodeMirror-rtl pre { direction: rtl; }

.CodeMirror-code {
  outline: none;
}

/* Force content-box sizing for the elements where we expect it */
.CodeMirror-scroll,
.CodeMirror-sizer,
.CodeMirror-gutter,
.CodeMirror-gutters,
.CodeMirror-linenumber {
  -moz-box-sizing: content-box;
  box-sizing: content-box;
}

.CodeMirror-measure {
  position: absolute;
  width: 100%;
  height: 0;
  overflow: hidden;
  visibility: hidden;
}

.CodeMirror-cursor {
  position: absolute;
  pointer-events: none;
}
.CodeMirror-measure pre { position: static; }

div.CodeMirror-cursors {
  visibility: hidden;
  position: relative;
  z-index: 3;
}
div.CodeMirror-dragcursors {
  visibility: visible;
}

.CodeMirror-focused div.CodeMirror-cursors {
  visibility: visible;
}

.CodeMirror-selected { background: #d9d9d9; }
.CodeMirror-focused .CodeMirror-selected { background: #d7d4f0; }
.CodeMirror-crosshair { cursor: crosshair; }
.CodeMirror-line::selection, .CodeMirror-line > span::selection, .CodeMirror-line > span > span::selection { background: #d7d4f0; }
.CodeMirror-line::-moz-selection, .CodeMirror-line > span::-moz-selection, .CodeMirror-line > span > span::-moz-selection { background: #d7d4f0; }

.cm-searching {
  background-color: #ffa;
  background-color: rgba(255, 255, 0, .4);
}

/* Used to force a border model for a node */
.cm-force-border { padding-right: .1px; }

@media print {
  /* Hide the cursor when printing */
  .CodeMirror div.CodeMirror-cursors {
    visibility: hidden;
  }
}

/* See issue #2901 */
.cm-tab-wrap-hack:after { content: ''; }

/* Help users use markselection to safely style text background */
span.CodeMirror-selectedtext { background: none; }

.CodeMirror-dialog {
  position: absolute;
  left: 0; right: 0;
  background: inherit;
  z-index: 15;
  padding: .1em .8em;
  overflow: hidden;
  color: inherit;
}

.CodeMirror-dialog-top {
  border-bottom: 1px solid #eee;
  top: 0;
}

.CodeMirror-dialog-bottom {
  border-top: 1px solid #eee;
  bottom: 0;
}

.CodeMirror-dialog input {
  border: none;
  outline: none;
  background: transparent;
  width: 20em;
  color: inherit;
  font-family: monospace;
}

.CodeMirror-dialog button {
  font-size: 70%;
}

.CodeMirror-foldmarker {
  color: blue;
  text-shadow: #b9f 1px 1px 2px, #b9f -1px -1px 2px, #b9f 1px -1px 2px, #b9f -1px 1px 2px;
  font-family: arial;
  line-height: .3;
  cursor: pointer;
}
.CodeMirror-foldgutter {
  width: .7em;
}
.CodeMirror-foldgutter-open,
.CodeMirror-foldgutter-folded {
  cursor: pointer;
}
.CodeMirror-foldgutter-open:after {
  content: "\25BE";
}
.CodeMirror-foldgutter-folded:after {
  content: "\25B8";
}

/*
  Name:       material
  Author:     Mattia Astorino (http://github.com/equinusocio)
  Website:    https://material-theme.site/
*/

.cm-s-material.CodeMirror {
  background-color: #263238;
  color: #EEFFFF;
}

.cm-s-material .CodeMirror-gutters {
  background: #263238;
  color: #546E7A;
  border: none;
}

.cm-s-material .CodeMirror-guttermarker,
.cm-s-material .CodeMirror-guttermarker-subtle,
.cm-s-material .CodeMirror-linenumber {
  color: #546E7A;
}

.cm-s-material .CodeMirror-cursor {
  border-left: 1px solid #FFCC00;
}

.cm-s-material div.CodeMirror-selected {
  background: rgba(128, 203, 196, 0.2);
}

.cm-s-material.CodeMirror-focused div.CodeMirror-selected {
  background: rgba(128, 203, 196, 0.2);
}

.cm-s-material .CodeMirror-line::selection,
.cm-s-material .CodeMirror-line>span::selection,
.cm-s-material .CodeMirror-line>span>span::selection {
  background: rgba(128, 203, 196, 0.2);
}

.cm-s-material .CodeMirror-line::-moz-selection,
.cm-s-material .CodeMirror-line>span::-moz-selection,
.cm-s-material .CodeMirror-line>span>span::-moz-selection {
  background: rgba(128, 203, 196, 0.2);
}

.cm-s-material .CodeMirror-activeline-background {
  background: rgba(0, 0, 0, 0.5);
}

.cm-s-material .cm-keyword {
  color: #C792EA;
}

.cm-s-material .cm-operator {
  color: #89DDFF;
}

.cm-s-material .cm-variable-2 {
  color: #EEFFFF;
}

.cm-s-material .cm-variable-3,
.cm-s-material .cm-type {
  color: #f07178;
}

.cm-s-material .cm-builtin {
  color: #FFCB6B;
}

.cm-s-material .cm-atom {
  color: #F78C6C;
}

.cm-s-material .cm-number {
  color: #FF5370;
}

.cm-s-material .cm-def {
  color: #82AAFF;
}

.cm-s-material .cm-string {
  color: #C3E88D;
}

.cm-s-material .cm-string-2 {
  color: #f07178;
}

.cm-s-material .cm-comment {
  color: #546E7A;
}

.cm-s-material .cm-variable {
  color: #f07178;
}

.cm-s-material .cm-tag {
  color: #FF5370;
}

.cm-s-material .cm-meta {
  color: #FFCB6B;
}

.cm-s-material .cm-attribute {
  color: #C792EA;
}

.cm-s-material .cm-property {
  color: #C792EA;
}

.cm-s-material .cm-qualifier {
  color: #DECB6B;
}

.cm-s-material .cm-variable-3,
.cm-s-material .cm-type {
  color: #DECB6B;
}


.cm-s-material .cm-error {
  color: rgba(255, 255, 255, 1.0);
  background-color: #FF5370;
}

.cm-s-material .CodeMirror-matchingbracket {
  text-decoration: underline;
  color: white !important;
}
/**
 * "
 *  Using Zenburn color palette from the Emacs Zenburn Theme
 *  https://github.com/bbatsov/zenburn-emacs/blob/master/zenburn-theme.el
 *
 *  Also using parts of https://github.com/xavi/coderay-lighttable-theme
 * "
 * From: https://github.com/wisenomad/zenburn-lighttable-theme/blob/master/zenburn.css
 */

.cm-s-zenburn .CodeMirror-gutters { background: #3f3f3f !important; }
.cm-s-zenburn .CodeMirror-foldgutter-open, .CodeMirror-foldgutter-folded { color: #999; }
.cm-s-zenburn .CodeMirror-cursor { border-left: 1px solid white; }
.cm-s-zenburn { background-color: #3f3f3f; color: #dcdccc; }
.cm-s-zenburn span.cm-builtin { color: #dcdccc; font-weight: bold; }
.cm-s-zenburn span.cm-comment { color: #7f9f7f; }
.cm-s-zenburn span.cm-keyword { color: #f0dfaf; font-weight: bold; }
.cm-s-zenburn span.cm-atom { color: #bfebbf; }
.cm-s-zenburn span.cm-def { color: #dcdccc; }
.cm-s-zenburn span.cm-variable { color: #dfaf8f; }
.cm-s-zenburn span.cm-variable-2 { color: #dcdccc; }
.cm-s-zenburn span.cm-string { color: #cc9393; }
.cm-s-zenburn span.cm-string-2 { color: #cc9393; }
.cm-s-zenburn span.cm-number { color: #dcdccc; }
.cm-s-zenburn span.cm-tag { color: #93e0e3; }
.cm-s-zenburn span.cm-property { color: #dfaf8f; }
.cm-s-zenburn span.cm-attribute { color: #dfaf8f; }
.cm-s-zenburn span.cm-qualifier { color: #7cb8bb; }
.cm-s-zenburn span.cm-meta { color: #f0dfaf; }
.cm-s-zenburn span.cm-header { color: #f0efd0; }
.cm-s-zenburn span.cm-operator { color: #f0efd0; }
.cm-s-zenburn span.CodeMirror-matchingbracket { box-sizing: border-box; background: transparent; border-bottom: 1px solid; }
.cm-s-zenburn span.CodeMirror-nonmatchingbracket { border-bottom: 1px solid; background: none; }
.cm-s-zenburn .CodeMirror-activeline { background: #000000; }
.cm-s-zenburn .CodeMirror-activeline-background { background: #000000; }
.cm-s-zenburn div.CodeMirror-selected { background: #545454; }
.cm-s-zenburn .CodeMirror-focused div.CodeMirror-selected { background: #4f4f4f; }

.cm-s-abcdef.CodeMirror { background: #0f0f0f; color: #defdef; }
.cm-s-abcdef div.CodeMirror-selected { background: #515151; }
.cm-s-abcdef .CodeMirror-line::selection, .cm-s-abcdef .CodeMirror-line > span::selection, .cm-s-abcdef .CodeMirror-line > span > span::selection { background: rgba(56, 56, 56, 0.99); }
.cm-s-abcdef .CodeMirror-line::-moz-selection, .cm-s-abcdef .CodeMirror-line > span::-moz-selection, .cm-s-abcdef .CodeMirror-line > span > span::-moz-selection { background: rgba(56, 56, 56, 0.99); }
.cm-s-abcdef .CodeMirror-gutters { background: #555; border-right: 2px solid #314151; }
.cm-s-abcdef .CodeMirror-guttermarker { color: #222; }
.cm-s-abcdef .CodeMirror-guttermarker-subtle { color: azure; }
.cm-s-abcdef .CodeMirror-linenumber { color: #FFFFFF; }
.cm-s-abcdef .CodeMirror-cursor { border-left: 1px solid #00FF00; }

.cm-s-abcdef span.cm-keyword { color: darkgoldenrod; font-weight: bold; }
.cm-s-abcdef span.cm-atom { color: #77F; }
.cm-s-abcdef span.cm-number { color: violet; }
.cm-s-abcdef span.cm-def { color: #fffabc; }
.cm-s-abcdef span.cm-variable { color: #abcdef; }
.cm-s-abcdef span.cm-variable-2 { color: #cacbcc; }
.cm-s-abcdef span.cm-variable-3, .cm-s-abcdef span.cm-type { color: #def; }
.cm-s-abcdef span.cm-property { color: #fedcba; }
.cm-s-abcdef span.cm-operator { color: #ff0; }
.cm-s-abcdef span.cm-comment { color: #7a7b7c; font-style: italic;}
.cm-s-abcdef span.cm-string { color: #2b4; }
.cm-s-abcdef span.cm-meta { color: #C9F; }
.cm-s-abcdef span.cm-qualifier { color: #FFF700; }
.cm-s-abcdef span.cm-builtin { color: #30aabc; }
.cm-s-abcdef span.cm-bracket { color: #8a8a8a; }
.cm-s-abcdef span.cm-tag { color: #FFDD44; }
.cm-s-abcdef span.cm-attribute { color: #DDFF00; }
.cm-s-abcdef span.cm-error { color: #FF0000; }
.cm-s-abcdef span.cm-header { color: aquamarine; font-weight: bold; }
.cm-s-abcdef span.cm-link { color: blueviolet; }

.cm-s-abcdef .CodeMirror-activeline-background { background: #314151; }

/*

    Name:       Base16 Default Light
    Author:     Chris Kempson (http://chriskempson.com)

    CodeMirror template by Jan T. Sott (https://github.com/idleberg/base16-codemirror)
    Original Base16 color scheme by Chris Kempson (https://github.com/chriskempson/base16)

*/

.cm-s-base16-light.CodeMirror { background: #f5f5f5; color: #202020; }
.cm-s-base16-light div.CodeMirror-selected { background: #e0e0e0; }
.cm-s-base16-light .CodeMirror-line::selection, .cm-s-base16-light .CodeMirror-line > span::selection, .cm-s-base16-light .CodeMirror-line > span > span::selection { background: #e0e0e0; }
.cm-s-base16-light .CodeMirror-line::-moz-selection, .cm-s-base16-light .CodeMirror-line > span::-moz-selection, .cm-s-base16-light .CodeMirror-line > span > span::-moz-selection { background: #e0e0e0; }
.cm-s-base16-light .CodeMirror-gutters { background: #f5f5f5; border-right: 0px; }
.cm-s-base16-light .CodeMirror-guttermarker { color: #ac4142; }
.cm-s-base16-light .CodeMirror-guttermarker-subtle { color: #b0b0b0; }
.cm-s-base16-light .CodeMirror-linenumber { color: #b0b0b0; }
.cm-s-base16-light .CodeMirror-cursor { border-left: 1px solid #505050; }

.cm-s-base16-light span.cm-comment { color: #8f5536; }
.cm-s-base16-light span.cm-atom { color: #aa759f; }
.cm-s-base16-light span.cm-number { color: #aa759f; }

.cm-s-base16-light span.cm-property, .cm-s-base16-light span.cm-attribute { color: #90a959; }
.cm-s-base16-light span.cm-keyword { color: #ac4142; }
.cm-s-base16-light span.cm-string { color: #f4bf75; }

.cm-s-base16-light span.cm-variable { color: #90a959; }
.cm-s-base16-light span.cm-variable-2 { color: #6a9fb5; }
.cm-s-base16-light span.cm-def { color: #d28445; }
.cm-s-base16-light span.cm-bracket { color: #202020; }
.cm-s-base16-light span.cm-tag { color: #ac4142; }
.cm-s-base16-light span.cm-link { color: #aa759f; }
.cm-s-base16-light span.cm-error { background: #ac4142; color: #505050; }

.cm-s-base16-light .CodeMirror-activeline-background { background: #DDDCDC; }
.cm-s-base16-light .CodeMirror-matchingbracket { color: #f5f5f5 !important; background-color: #6A9FB5 !important}

/*

    Name:       Base16 Default Dark
    Author:     Chris Kempson (http://chriskempson.com)

    CodeMirror template by Jan T. Sott (https://github.com/idleberg/base16-codemirror)
    Original Base16 color scheme by Chris Kempson (https://github.com/chriskempson/base16)

*/

.cm-s-base16-dark.CodeMirror { background: #151515; color: #e0e0e0; }
.cm-s-base16-dark div.CodeMirror-selected { background: #303030; }
.cm-s-base16-dark .CodeMirror-line::selection, .cm-s-base16-dark .CodeMirror-line > span::selection, .cm-s-base16-dark .CodeMirror-line > span > span::selection { background: rgba(48, 48, 48, .99); }
.cm-s-base16-dark .CodeMirror-line::-moz-selection, .cm-s-base16-dark .CodeMirror-line > span::-moz-selection, .cm-s-base16-dark .CodeMirror-line > span > span::-moz-selection { background: rgba(48, 48, 48, .99); }
.cm-s-base16-dark .CodeMirror-gutters { background: #151515; border-right: 0px; }
.cm-s-base16-dark .CodeMirror-guttermarker { color: #ac4142; }
.cm-s-base16-dark .CodeMirror-guttermarker-subtle { color: #505050; }
.cm-s-base16-dark .CodeMirror-linenumber { color: #505050; }
.cm-s-base16-dark .CodeMirror-cursor { border-left: 1px solid #b0b0b0; }

.cm-s-base16-dark span.cm-comment { color: #8f5536; }
.cm-s-base16-dark span.cm-atom { color: #aa759f; }
.cm-s-base16-dark span.cm-number { color: #aa759f; }

.cm-s-base16-dark span.cm-property, .cm-s-base16-dark span.cm-attribute { color: #90a959; }
.cm-s-base16-dark span.cm-keyword { color: #ac4142; }
.cm-s-base16-dark span.cm-string { color: #f4bf75; }

.cm-s-base16-dark span.cm-variable { color: #90a959; }
.cm-s-base16-dark span.cm-variable-2 { color: #6a9fb5; }
.cm-s-base16-dark span.cm-def { color: #d28445; }
.cm-s-base16-dark span.cm-bracket { color: #e0e0e0; }
.cm-s-base16-dark span.cm-tag { color: #ac4142; }
.cm-s-base16-dark span.cm-link { color: #aa759f; }
.cm-s-base16-dark span.cm-error { background: #ac4142; color: #b0b0b0; }

.cm-s-base16-dark .CodeMirror-activeline-background { background: #202020; }
.cm-s-base16-dark .CodeMirror-matchingbracket { text-decoration: underline; color: white !important; }

/*

    Name:       dracula
    Author:     Michael Kaminsky (http://github.com/mkaminsky11)

    Original dracula color scheme by Zeno Rocha (https://github.com/zenorocha/dracula-theme)

*/


.cm-s-dracula.CodeMirror, .cm-s-dracula .CodeMirror-gutters {
  background-color: #282a36 !important;
  color: #f8f8f2 !important;
  border: none;
}
.cm-s-dracula .CodeMirror-gutters { color: #282a36; }
.cm-s-dracula .CodeMirror-cursor { border-left: solid thin #f8f8f0; }
.cm-s-dracula .CodeMirror-linenumber { color: #6D8A88; }
.cm-s-dracula .CodeMirror-selected { background: rgba(255, 255, 255, 0.10); }
.cm-s-dracula .CodeMirror-line::selection, .cm-s-dracula .CodeMirror-line > span::selection, .cm-s-dracula .CodeMirror-line > span > span::selection { background: rgba(255, 255, 255, 0.10); }
.cm-s-dracula .CodeMirror-line::-moz-selection, .cm-s-dracula .CodeMirror-line > span::-moz-selection, .cm-s-dracula .CodeMirror-line > span > span::-moz-selection { background: rgba(255, 255, 255, 0.10); }
.cm-s-dracula span.cm-comment { color: #6272a4; }
.cm-s-dracula span.cm-string, .cm-s-dracula span.cm-string-2 { color: #f1fa8c; }
.cm-s-dracula span.cm-number { color: #bd93f9; }
.cm-s-dracula span.cm-variable { color: #50fa7b; }
.cm-s-dracula span.cm-variable-2 { color: white; }
.cm-s-dracula span.cm-def { color: #50fa7b; }
.cm-s-dracula span.cm-operator { color: #ff79c6; }
.cm-s-dracula span.cm-keyword { color: #ff79c6; }
.cm-s-dracula span.cm-atom { color: #bd93f9; }
.cm-s-dracula span.cm-meta { color: #f8f8f2; }
.cm-s-dracula span.cm-tag { color: #ff79c6; }
.cm-s-dracula span.cm-attribute { color: #50fa7b; }
.cm-s-dracula span.cm-qualifier { color: #50fa7b; }
.cm-s-dracula span.cm-property { color: #66d9ef; }
.cm-s-dracula span.cm-builtin { color: #50fa7b; }
.cm-s-dracula span.cm-variable-3, .cm-s-dracula span.cm-type { color: #ffb86c; }

.cm-s-dracula .CodeMirror-activeline-background { background: rgba(255,255,255,0.1); }
.cm-s-dracula .CodeMirror-matchingbracket { text-decoration: underline; color: white !important; }

/*

    Name:       Hopscotch
    Author:     Jan T. Sott

    CodeMirror template by Jan T. Sott (https://github.com/idleberg/base16-codemirror)
    Original Base16 color scheme by Chris Kempson (https://github.com/chriskempson/base16)

*/

.cm-s-hopscotch.CodeMirror {background: #322931; color: #d5d3d5;}
.cm-s-hopscotch div.CodeMirror-selected {background: #433b42 !important;}
.cm-s-hopscotch .CodeMirror-gutters {background: #322931; border-right: 0px;}
.cm-s-hopscotch .CodeMirror-linenumber {color: #797379;}
.cm-s-hopscotch .CodeMirror-cursor {border-left: 1px solid #989498 !important;}

.cm-s-hopscotch span.cm-comment {color: #b33508;}
.cm-s-hopscotch span.cm-atom {color: #c85e7c;}
.cm-s-hopscotch span.cm-number {color: #c85e7c;}

.cm-s-hopscotch span.cm-property, .cm-s-hopscotch span.cm-attribute {color: #8fc13e;}
.cm-s-hopscotch span.cm-keyword {color: #dd464c;}
.cm-s-hopscotch span.cm-string {color: #fdcc59;}

.cm-s-hopscotch span.cm-variable {color: #8fc13e;}
.cm-s-hopscotch span.cm-variable-2 {color: #1290bf;}
.cm-s-hopscotch span.cm-def {color: #fd8b19;}
.cm-s-hopscotch span.cm-error {background: #dd464c; color: #989498;}
.cm-s-hopscotch span.cm-bracket {color: #d5d3d5;}
.cm-s-hopscotch span.cm-tag {color: #dd464c;}
.cm-s-hopscotch span.cm-link {color: #c85e7c;}

.cm-s-hopscotch .CodeMirror-matchingbracket { text-decoration: underline; color: white !important;}
.cm-s-hopscotch .CodeMirror-activeline-background { background: #302020; }

/****************************************************************/
/*   Based on mbonaci's Brackets mbo theme                      */
/*   https://github.com/mbonaci/global/blob/master/Mbo.tmTheme  */
/*   Create your own: http://tmtheme-editor.herokuapp.com       */
/****************************************************************/

.cm-s-mbo.CodeMirror { background: #2c2c2c; color: #ffffec; }
.cm-s-mbo div.CodeMirror-selected { background: #716C62; }
.cm-s-mbo .CodeMirror-line::selection, .cm-s-mbo .CodeMirror-line > span::selection, .cm-s-mbo .CodeMirror-line > span > span::selection { background: rgba(113, 108, 98, .99); }
.cm-s-mbo .CodeMirror-line::-moz-selection, .cm-s-mbo .CodeMirror-line > span::-moz-selection, .cm-s-mbo .CodeMirror-line > span > span::-moz-selection { background: rgba(113, 108, 98, .99); }
.cm-s-mbo .CodeMirror-gutters { background: #4e4e4e; border-right: 0px; }
.cm-s-mbo .CodeMirror-guttermarker { color: white; }
.cm-s-mbo .CodeMirror-guttermarker-subtle { color: grey; }
.cm-s-mbo .CodeMirror-linenumber { color: #dadada; }
.cm-s-mbo .CodeMirror-cursor { border-left: 1px solid #ffffec; }

.cm-s-mbo span.cm-comment { color: #95958a; }
.cm-s-mbo span.cm-atom { color: #00a8c6; }
.cm-s-mbo span.cm-number { color: #00a8c6; }

.cm-s-mbo span.cm-property, .cm-s-mbo span.cm-attribute { color: #9ddfe9; }
.cm-s-mbo span.cm-keyword { color: #ffb928; }
.cm-s-mbo span.cm-string { color: #ffcf6c; }
.cm-s-mbo span.cm-string.cm-property { color: #ffffec; }

.cm-s-mbo span.cm-variable { color: #ffffec; }
.cm-s-mbo span.cm-variable-2 { color: #00a8c6; }
.cm-s-mbo span.cm-def { color: #ffffec; }
.cm-s-mbo span.cm-bracket { color: #fffffc; font-weight: bold; }
.cm-s-mbo span.cm-tag { color: #9ddfe9; }
.cm-s-mbo span.cm-link { color: #f54b07; }
.cm-s-mbo span.cm-error { border-bottom: #636363; color: #ffffec; }
.cm-s-mbo span.cm-qualifier { color: #ffffec; }

.cm-s-mbo .CodeMirror-activeline-background { background: #494b41; }
.cm-s-mbo .CodeMirror-matchingbracket { color: #ffb928 !important; }
.cm-s-mbo .CodeMirror-matchingtag { background: rgba(255, 255, 255, .37); }

/*
  MDN-LIKE Theme - Mozilla
  Ported to CodeMirror by Peter Kroon <plakroon@gmail.com>
  Report bugs/issues here: https://github.com/codemirror/CodeMirror/issues
  GitHub: @peterkroon

  The mdn-like theme is inspired on the displayed code examples at: https://developer.mozilla.org/en-US/docs/Web/CSS/animation

*/
.cm-s-mdn-like.CodeMirror { color: #999; background-color: #fff; }
.cm-s-mdn-like div.CodeMirror-selected { background: #cfc; }
.cm-s-mdn-like .CodeMirror-line::selection, .cm-s-mdn-like .CodeMirror-line > span::selection, .cm-s-mdn-like .CodeMirror-line > span > span::selection { background: #cfc; }
.cm-s-mdn-like .CodeMirror-line::-moz-selection, .cm-s-mdn-like .CodeMirror-line > span::-moz-selection, .cm-s-mdn-like .CodeMirror-line > span > span::-moz-selection { background: #cfc; }

.cm-s-mdn-like .CodeMirror-gutters { background: #f8f8f8; border-left: 6px solid rgba(0,83,159,0.65); color: #333; }
.cm-s-mdn-like .CodeMirror-linenumber { color: #aaa; padding-left: 8px; }
.cm-s-mdn-like .CodeMirror-cursor { border-left: 2px solid #222; }

.cm-s-mdn-like .cm-keyword { color: #6262FF; }
.cm-s-mdn-like .cm-atom { color: #F90; }
.cm-s-mdn-like .cm-number { color:  #ca7841; }
.cm-s-mdn-like .cm-def { color: #8DA6CE; }
.cm-s-mdn-like span.cm-variable-2, .cm-s-mdn-like span.cm-tag { color: #690; }
.cm-s-mdn-like span.cm-variable-3, .cm-s-mdn-like span.cm-def, .cm-s-mdn-like span.cm-type { color: #07a; }

.cm-s-mdn-like .cm-variable { color: #07a; }
.cm-s-mdn-like .cm-property { color: #905; }
.cm-s-mdn-like .cm-qualifier { color: #690; }

.cm-s-mdn-like .cm-operator { color: #cda869; }
.cm-s-mdn-like .cm-comment { color:#777; font-weight:normal; }
.cm-s-mdn-like .cm-string { color:#07a; font-style:italic; }
.cm-s-mdn-like .cm-string-2 { color:#bd6b18; } /*?*/
.cm-s-mdn-like .cm-meta { color: #000; } /*?*/
.cm-s-mdn-like .cm-builtin { color: #9B7536; } /*?*/
.cm-s-mdn-like .cm-tag { color: #997643; }
.cm-s-mdn-like .cm-attribute { color: #d6bb6d; } /*?*/
.cm-s-mdn-like .cm-header { color: #FF6400; }
.cm-s-mdn-like .cm-hr { color: #AEAEAE; }
.cm-s-mdn-like .cm-link { color:#ad9361; font-style:italic; text-decoration:none; }
.cm-s-mdn-like .cm-error { border-bottom: 1px solid red; }

div.cm-s-mdn-like .CodeMirror-activeline-background { background: #efefff; }
div.cm-s-mdn-like span.CodeMirror-matchingbracket { outline:1px solid grey; color: inherit; }

.cm-s-mdn-like.CodeMirror { background-image: url(data:image/png;base64,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); }

/*

    Name:       seti
    Author:     Michael Kaminsky (http://github.com/mkaminsky11)

    Original seti color scheme by Jesse Weed (https://github.com/jesseweed/seti-syntax)

*/


.cm-s-seti.CodeMirror {
  background-color: #151718 !important;
  color: #CFD2D1 !important;
  border: none;
}
.cm-s-seti .CodeMirror-gutters {
  color: #404b53;
  background-color: #0E1112;
  border: none;
}
.cm-s-seti .CodeMirror-cursor { border-left: solid thin #f8f8f0; }
.cm-s-seti .CodeMirror-linenumber { color: #6D8A88; }
.cm-s-seti.CodeMirror-focused div.CodeMirror-selected { background: rgba(255, 255, 255, 0.10); }
.cm-s-seti .CodeMirror-line::selection, .cm-s-seti .CodeMirror-line > span::selection, .cm-s-seti .CodeMirror-line > span > span::selection { background: rgba(255, 255, 255, 0.10); }
.cm-s-seti .CodeMirror-line::-moz-selection, .cm-s-seti .CodeMirror-line > span::-moz-selection, .cm-s-seti .CodeMirror-line > span > span::-moz-selection { background: rgba(255, 255, 255, 0.10); }
.cm-s-seti span.cm-comment { color: #41535b; }
.cm-s-seti span.cm-string, .cm-s-seti span.cm-string-2 { color: #55b5db; }
.cm-s-seti span.cm-number { color: #cd3f45; }
.cm-s-seti span.cm-variable { color: #55b5db; }
.cm-s-seti span.cm-variable-2 { color: #a074c4; }
.cm-s-seti span.cm-def { color: #55b5db; }
.cm-s-seti span.cm-keyword { color: #ff79c6; }
.cm-s-seti span.cm-operator { color: #9fca56; }
.cm-s-seti span.cm-keyword { color: #e6cd69; }
.cm-s-seti span.cm-atom { color: #cd3f45; }
.cm-s-seti span.cm-meta { color: #55b5db; }
.cm-s-seti span.cm-tag { color: #55b5db; }
.cm-s-seti span.cm-attribute { color: #9fca56; }
.cm-s-seti span.cm-qualifier { color: #9fca56; }
.cm-s-seti span.cm-property { color: #a074c4; }
.cm-s-seti span.cm-variable-3, .cm-s-seti span.cm-type { color: #9fca56; }
.cm-s-seti span.cm-builtin { color: #9fca56; }
.cm-s-seti .CodeMirror-activeline-background { background: #101213; }
.cm-s-seti .CodeMirror-matchingbracket { text-decoration: underline; color: white !important; }

/*
Solarized theme for code-mirror
http://ethanschoonover.com/solarized
*/

/*
Solarized color palette
http://ethanschoonover.com/solarized/img/solarized-palette.png
*/

.solarized.base03 { color: #002b36; }
.solarized.base02 { color: #073642; }
.solarized.base01 { color: #586e75; }
.solarized.base00 { color: #657b83; }
.solarized.base0 { color: #839496; }
.solarized.base1 { color: #93a1a1; }
.solarized.base2 { color: #eee8d5; }
.solarized.base3  { color: #fdf6e3; }
.solarized.solar-yellow  { color: #b58900; }
.solarized.solar-orange  { color: #cb4b16; }
.solarized.solar-red { color: #dc322f; }
.solarized.solar-magenta { color: #d33682; }
.solarized.solar-violet  { color: #6c71c4; }
.solarized.solar-blue { color: #268bd2; }
.solarized.solar-cyan { color: #2aa198; }
.solarized.solar-green { color: #859900; }

/* Color scheme for code-mirror */

.cm-s-solarized {
  line-height: 1.45em;
  color-profile: sRGB;
  rendering-intent: auto;
}
.cm-s-solarized.cm-s-dark {
  color: #839496;
  background-color: #002b36;
  text-shadow: #002b36 0 1px;
}
.cm-s-solarized.cm-s-light {
  background-color: #fdf6e3;
  color: #657b83;
  text-shadow: #eee8d5 0 1px;
}

.cm-s-solarized .CodeMirror-widget {
  text-shadow: none;
}

.cm-s-solarized .cm-header { color: #586e75; }
.cm-s-solarized .cm-quote { color: #93a1a1; }

.cm-s-solarized .cm-keyword { color: #cb4b16; }
.cm-s-solarized .cm-atom { color: #d33682; }
.cm-s-solarized .cm-number { color: #d33682; }
.cm-s-solarized .cm-def { color: #2aa198; }

.cm-s-solarized .cm-variable { color: #839496; }
.cm-s-solarized .cm-variable-2 { color: #b58900; }
.cm-s-solarized .cm-variable-3, .cm-s-solarized .cm-type { color: #6c71c4; }

.cm-s-solarized .cm-property { color: #2aa198; }
.cm-s-solarized .cm-operator { color: #6c71c4; }

.cm-s-solarized .cm-comment { color: #586e75; font-style:italic; }

.cm-s-solarized .cm-string { color: #859900; }
.cm-s-solarized .cm-string-2 { color: #b58900; }

.cm-s-solarized .cm-meta { color: #859900; }
.cm-s-solarized .cm-qualifier { color: #b58900; }
.cm-s-solarized .cm-builtin { color: #d33682; }
.cm-s-solarized .cm-bracket { color: #cb4b16; }
.cm-s-solarized .CodeMirror-matchingbracket { color: #859900; }
.cm-s-solarized .CodeMirror-nonmatchingbracket { color: #dc322f; }
.cm-s-solarized .cm-tag { color: #93a1a1; }
.cm-s-solarized .cm-attribute { color: #2aa198; }
.cm-s-solarized .cm-hr {
  color: transparent;
  border-top: 1px solid #586e75;
  display: block;
}
.cm-s-solarized .cm-link { color: #93a1a1; cursor: pointer; }
.cm-s-solarized .cm-special { color: #6c71c4; }
.cm-s-solarized .cm-em {
  color: #999;
  text-decoration: underline;
  text-decoration-style: dotted;
}
.cm-s-solarized .cm-error,
.cm-s-solarized .cm-invalidchar {
  color: #586e75;
  border-bottom: 1px dotted #dc322f;
}

.cm-s-solarized.cm-s-dark div.CodeMirror-selected { background: #073642; }
.cm-s-solarized.cm-s-dark.CodeMirror ::selection { background: rgba(7, 54, 66, 0.99); }
.cm-s-solarized.cm-s-dark .CodeMirror-line::-moz-selection, .cm-s-dark .CodeMirror-line > span::-moz-selection, .cm-s-dark .CodeMirror-line > span > span::-moz-selection { background: rgba(7, 54, 66, 0.99); }

.cm-s-solarized.cm-s-light div.CodeMirror-selected { background: #eee8d5; }
.cm-s-solarized.cm-s-light .CodeMirror-line::selection, .cm-s-light .CodeMirror-line > span::selection, .cm-s-light .CodeMirror-line > span > span::selection { background: #eee8d5; }
.cm-s-solarized.cm-s-light .CodeMirror-line::-moz-selection, .cm-s-ligh .CodeMirror-line > span::-moz-selection, .cm-s-ligh .CodeMirror-line > span > span::-moz-selection { background: #eee8d5; }

/* Editor styling */



/* Little shadow on the view-port of the buffer view */
.cm-s-solarized.CodeMirror {
  -moz-box-shadow: inset 7px 0 12px -6px #000;
  -webkit-box-shadow: inset 7px 0 12px -6px #000;
  box-shadow: inset 7px 0 12px -6px #000;
}

/* Remove gutter border */
.cm-s-solarized .CodeMirror-gutters {
  border-right: 0;
}

/* Gutter colors and line number styling based of color scheme (dark / light) */

/* Dark */
.cm-s-solarized.cm-s-dark .CodeMirror-gutters {
  background-color: #073642;
}

.cm-s-solarized.cm-s-dark .CodeMirror-linenumber {
  color: #586e75;
  text-shadow: #021014 0 -1px;
}

/* Light */
.cm-s-solarized.cm-s-light .CodeMirror-gutters {
  background-color: #eee8d5;
}

.cm-s-solarized.cm-s-light .CodeMirror-linenumber {
  color: #839496;
}

/* Common */
.cm-s-solarized .CodeMirror-linenumber {
  padding: 0 5px;
}
.cm-s-solarized .CodeMirror-guttermarker-subtle { color: #586e75; }
.cm-s-solarized.cm-s-dark .CodeMirror-guttermarker { color: #ddd; }
.cm-s-solarized.cm-s-light .CodeMirror-guttermarker { color: #cb4b16; }

.cm-s-solarized .CodeMirror-gutter .CodeMirror-gutter-text {
  color: #586e75;
}

/* Cursor */
.cm-s-solarized .CodeMirror-cursor { border-left: 1px solid #819090; }

/* Fat cursor */
.cm-s-solarized.cm-s-light.cm-fat-cursor .CodeMirror-cursor { background: #77ee77; }
.cm-s-solarized.cm-s-light .cm-animate-fat-cursor { background-color: #77ee77; }
.cm-s-solarized.cm-s-dark.cm-fat-cursor .CodeMirror-cursor { background: #586e75; }
.cm-s-solarized.cm-s-dark .cm-animate-fat-cursor { background-color: #586e75; }

/* Active line */
.cm-s-solarized.cm-s-dark .CodeMirror-activeline-background {
  background: rgba(255, 255, 255, 0.06);
}
.cm-s-solarized.cm-s-light .CodeMirror-activeline-background {
  background: rgba(0, 0, 0, 0.06);
}

.cm-s-the-matrix.CodeMirror { background: #000000; color: #00FF00; }
.cm-s-the-matrix div.CodeMirror-selected { background: #2D2D2D; }
.cm-s-the-matrix .CodeMirror-line::selection, .cm-s-the-matrix .CodeMirror-line > span::selection, .cm-s-the-matrix .CodeMirror-line > span > span::selection { background: rgba(45, 45, 45, 0.99); }
.cm-s-the-matrix .CodeMirror-line::-moz-selection, .cm-s-the-matrix .CodeMirror-line > span::-moz-selection, .cm-s-the-matrix .CodeMirror-line > span > span::-moz-selection { background: rgba(45, 45, 45, 0.99); }
.cm-s-the-matrix .CodeMirror-gutters { background: #060; border-right: 2px solid #00FF00; }
.cm-s-the-matrix .CodeMirror-guttermarker { color: #0f0; }
.cm-s-the-matrix .CodeMirror-guttermarker-subtle { color: white; }
.cm-s-the-matrix .CodeMirror-linenumber { color: #FFFFFF; }
.cm-s-the-matrix .CodeMirror-cursor { border-left: 1px solid #00FF00; }

.cm-s-the-matrix span.cm-keyword { color: #008803; font-weight: bold; }
.cm-s-the-matrix span.cm-atom { color: #3FF; }
.cm-s-the-matrix span.cm-number { color: #FFB94F; }
.cm-s-the-matrix span.cm-def { color: #99C; }
.cm-s-the-matrix span.cm-variable { color: #F6C; }
.cm-s-the-matrix span.cm-variable-2 { color: #C6F; }
.cm-s-the-matrix span.cm-variable-3, .cm-s-the-matrix span.cm-type { color: #96F; }
.cm-s-the-matrix span.cm-property { color: #62FFA0; }
.cm-s-the-matrix span.cm-operator { color: #999; }
.cm-s-the-matrix span.cm-comment { color: #CCCCCC; }
.cm-s-the-matrix span.cm-string { color: #39C; }
.cm-s-the-matrix span.cm-meta { color: #C9F; }
.cm-s-the-matrix span.cm-qualifier { color: #FFF700; }
.cm-s-the-matrix span.cm-builtin { color: #30a; }
.cm-s-the-matrix span.cm-bracket { color: #cc7; }
.cm-s-the-matrix span.cm-tag { color: #FFBD40; }
.cm-s-the-matrix span.cm-attribute { color: #FFF700; }
.cm-s-the-matrix span.cm-error { color: #FF0000; }

.cm-s-the-matrix .CodeMirror-activeline-background { background: #040; }

/*
Copyright (C) 2011 by MarkLogic Corporation
Author: Mike Brevoort <mike@brevoort.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
*/
.cm-s-xq-light span.cm-keyword { line-height: 1em; font-weight: bold; color: #5A5CAD; }
.cm-s-xq-light span.cm-atom { color: #6C8CD5; }
.cm-s-xq-light span.cm-number { color: #164; }
.cm-s-xq-light span.cm-def { text-decoration:underline; }
.cm-s-xq-light span.cm-variable { color: black; }
.cm-s-xq-light span.cm-variable-2 { color:black; }
.cm-s-xq-light span.cm-variable-3, .cm-s-xq-light span.cm-type { color: black; }
.cm-s-xq-light span.cm-property {}
.cm-s-xq-light span.cm-operator {}
.cm-s-xq-light span.cm-comment { color: #0080FF; font-style: italic; }
.cm-s-xq-light span.cm-string { color: red; }
.cm-s-xq-light span.cm-meta { color: yellow; }
.cm-s-xq-light span.cm-qualifier { color: grey; }
.cm-s-xq-light span.cm-builtin { color: #7EA656; }
.cm-s-xq-light span.cm-bracket { color: #cc7; }
.cm-s-xq-light span.cm-tag { color: #3F7F7F; }
.cm-s-xq-light span.cm-attribute { color: #7F007F; }
.cm-s-xq-light span.cm-error { color: #f00; }

.cm-s-xq-light .CodeMirror-activeline-background { background: #e8f2ff; }
.cm-s-xq-light .CodeMirror-matchingbracket { outline:1px solid grey;color:black !important;background:yellow; }

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.CodeMirror {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;
  /* Changed to auto to autogrow */
}

.CodeMirror pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

/* This causes https://github.com/jupyter/jupyterlab/issues/522 */
/* May not cause it not because we changed it! */
.CodeMirror-lines {
  padding: var(--jp-code-padding) 0;
}

.CodeMirror-linenumber {
  padding: 0 8px;
}

.jp-CodeMirrorEditor-static {
  margin: var(--jp-code-padding);
}

.jp-CodeMirrorEditor,
.jp-CodeMirrorEditor-static {
  cursor: text;
}

.jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
  border-left: var(--jp-code-cursor-width0) solid var(--jp-editor-cursor-color);
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.CodeMirror.jp-mod-readOnly .CodeMirror-cursor {
  display: none;
}

.CodeMirror-gutters {
  border-right: 1px solid var(--jp-border-color2);
  background-color: var(--jp-layout-color0);
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.CodeMirror-selectedtext.cm-searching {
  background-color: var(--jp-search-selected-match-background-color) !important;
  color: var(--jp-search-selected-match-color) !important;
}

.cm-searching {
  background-color: var(
    --jp-search-unselected-match-background-color
  ) !important;
  color: var(--jp-search-unselected-match-color) !important;
}

.CodeMirror-focused .CodeMirror-selected {
  background-color: var(--jp-editor-selected-focused-background);
}

.CodeMirror-selected {
  background-color: var(--jp-editor-selected-background);
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/**
 * Here is our jupyter theme for CodeMirror syntax highlighting
 * This is used in our marked.js syntax highlighting and CodeMirror itself
 * The string "jupyter" is set in ../codemirror/widget.DEFAULT_CODEMIRROR_THEME
 * This came from the classic notebook, which came form highlight.js/GitHub
 */

/**
 * CodeMirror themes are handling the background/color in this way. This works
 * fine for CodeMirror editors outside the notebook, but the notebook styles
 * these things differently.
 */
.CodeMirror.cm-s-jupyter {
  background: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

/* In the notebook, we want this styling to be handled by its container */
.jp-CodeConsole .CodeMirror.cm-s-jupyter,
.jp-Notebook .CodeMirror.cm-s-jupyter {
  background: transparent;
}

.cm-s-jupyter .CodeMirror-cursor {
  border-left: var(--jp-code-cursor-width0) solid var(--jp-editor-cursor-color);
}
.cm-s-jupyter span.cm-keyword {
  color: var(--jp-mirror-editor-keyword-color);
  font-weight: bold;
}
.cm-s-jupyter span.cm-atom {
  color: var(--jp-mirror-editor-atom-color);
}
.cm-s-jupyter span.cm-number {
  color: var(--jp-mirror-editor-number-color);
}
.cm-s-jupyter span.cm-def {
  color: var(--jp-mirror-editor-def-color);
}
.cm-s-jupyter span.cm-variable {
  color: var(--jp-mirror-editor-variable-color);
}
.cm-s-jupyter span.cm-variable-2 {
  color: var(--jp-mirror-editor-variable-2-color);
}
.cm-s-jupyter span.cm-variable-3 {
  color: var(--jp-mirror-editor-variable-3-color);
}
.cm-s-jupyter span.cm-punctuation {
  color: var(--jp-mirror-editor-punctuation-color);
}
.cm-s-jupyter span.cm-property {
  color: var(--jp-mirror-editor-property-color);
}
.cm-s-jupyter span.cm-operator {
  color: var(--jp-mirror-editor-operator-color);
  font-weight: bold;
}
.cm-s-jupyter span.cm-comment {
  color: var(--jp-mirror-editor-comment-color);
  font-style: italic;
}
.cm-s-jupyter span.cm-string {
  color: var(--jp-mirror-editor-string-color);
}
.cm-s-jupyter span.cm-string-2 {
  color: var(--jp-mirror-editor-string-2-color);
}
.cm-s-jupyter span.cm-meta {
  color: var(--jp-mirror-editor-meta-color);
}
.cm-s-jupyter span.cm-qualifier {
  color: var(--jp-mirror-editor-qualifier-color);
}
.cm-s-jupyter span.cm-builtin {
  color: var(--jp-mirror-editor-builtin-color);
}
.cm-s-jupyter span.cm-bracket {
  color: var(--jp-mirror-editor-bracket-color);
}
.cm-s-jupyter span.cm-tag {
  color: var(--jp-mirror-editor-tag-color);
}
.cm-s-jupyter span.cm-attribute {
  color: var(--jp-mirror-editor-attribute-color);
}
.cm-s-jupyter span.cm-header {
  color: var(--jp-mirror-editor-header-color);
}
.cm-s-jupyter span.cm-quote {
  color: var(--jp-mirror-editor-quote-color);
}
.cm-s-jupyter span.cm-link {
  color: var(--jp-mirror-editor-link-color);
}
.cm-s-jupyter span.cm-error {
  color: var(--jp-mirror-editor-error-color);
}
.cm-s-jupyter span.cm-hr {
  color: #999;
}

.cm-s-jupyter span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}

.cm-s-jupyter .CodeMirror-activeline-background,
.cm-s-jupyter .CodeMirror-gutter {
  background-color: var(--jp-layout-color2);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0px;
  padding: 0px;
  line-height: normal;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}
.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}
.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}
.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}
.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}
.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}
.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}
.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}
.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}
.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
}
.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
}
.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
}
.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
}
.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
}
.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
}
.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
}
.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}
.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}
.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}
.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}
.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}
.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}
.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}
.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
}
.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
}
.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
}
.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
}
.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
}
.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
}
.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
}
.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}
.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}
.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0em;
}

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: 12px;
  table-layout: fixed;
  margin-left: auto;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon table {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0px;
}

.jp-RenderedHTMLCommon p {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}
[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}
/* ...or leave it untouched if they don't */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-dark-background {
}
[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-light-background {
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}
.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}
.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}
.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}
.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}
.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}
.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}
.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}
.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: 0.8em;
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser {
  display: flex;
  flex-direction: column;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  border-bottom: none;
  height: auto;
  margin: var(--jp-toolbar-header-margin);
  box-shadow: none;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 4px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0px 2px;
  padding: 0px 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0px;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar.jp-Toolbar {
  padding: 0px;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  justify-content: space-evenly;
}

.jp-FileBrowser-toolbar.jp-Toolbar .jp-Toolbar-item {
  flex: 1;
}

.jp-FileBrowser-toolbar.jp-Toolbar .jp-ToolbarButtonComponent {
  width: 100%;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px 12px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-item.jp-mod-selected {
  color: white;
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon:before {
  color: limegreen;
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0px;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-DirListing-deadSpace {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

.jp-FileDialog.jp-mod-conflict input {
  color: red;
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
}

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: flex;
  flex-direction: row;
}

.jp-OutputPrompt {
  flex: 0 0 var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);
  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-OutputArea-output {
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea-child .jp-OutputArea-output {
  flex-grow: 1;
  flex-shrink: 1;
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `p-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0px;
  padding: 0px;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0px;
  flex: 1 1 auto;
}

.jp-OutputArea-executeResult.jp-RenderedText {
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-OutputArea-stdin {
  line-height: var(--jp-code-line-height);
  padding-top: var(--jp-code-padding);
  display: flex;
}

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0px;
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;
  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0px;
  bottom: 0px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0px;
  width: 100%;
  padding: 0px;
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: flex;
  flex-direction: row;
}

.jp-InputArea-editor {
  flex: 1 1 auto;
}

.jp-InputArea-editor {
  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0px;
  background: var(--jp-cell-editor-background);
}

.jp-InputPrompt {
  flex: 0 0 var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);
  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: flex;
  flex-direction: row;
  flex: 1 1 auto;
}

.jp-Placeholder-prompt {
  box-sizing: border-box;
}

.jp-Placeholder-content {
  flex: 1 1 auto;
  border: none;
  background: transparent;
  height: 20px;
  box-sizing: border-box;
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0px 0px 2px 0px rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0px;
  margin: 0px;
  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 200px;
  box-shadow: inset 0 0 6px 2px rgba(0, 0, 0, 0.3);
  margin-left: var(--jp-private-cell-scrolling-output-offset);
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  flex: 0 0
    calc(
      var(--jp-cell-prompt-width) -
        var(--jp-private-cell-scrolling-output-offset)
    );
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  flex: 1 1 auto;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: 2px;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: flex;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0px rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0px;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0px rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-NotebookTools-tool {
  padding: 0px 12px 0 12px;
}

.jp-ActiveCellTool {
  padding: 12px;
  background-color: var(--jp-layout-color1);
  border-top: none !important;
}

.jp-ActiveCellTool .jp-InputArea-prompt {
  flex: 0 0 auto;
  padding-left: 0px;
}

.jp-ActiveCellTool .jp-InputArea-editor {
  flex: 1 1 auto;
  background: var(--jp-cell-editor-background);
  border-color: var(--jp-cell-editor-border-color);
}

.jp-ActiveCellTool .jp-InputArea-editor .CodeMirror {
  background: transparent;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0px 12px 0px;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label {
  line-height: 1.4;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensurePackage() in @jupyterlab/buildutils */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

</style>

    <style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

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

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0px 2px 1px -1px var(--jp-shadow-umbra-color),
    0px 1px 1px 0px var(--jp-shadow-penumbra-color),
    0px 1px 3px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0px 3px 1px -2px var(--jp-shadow-umbra-color),
    0px 2px 2px 0px var(--jp-shadow-penumbra-color),
    0px 1px 5px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0px 2px 4px -1px var(--jp-shadow-umbra-color),
    0px 4px 5px 0px var(--jp-shadow-penumbra-color),
    0px 1px 10px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0px 3px 5px -1px var(--jp-shadow-umbra-color),
    0px 6px 10px 0px var(--jp-shadow-penumbra-color),
    0px 1px 18px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0px 5px 5px -3px var(--jp-shadow-umbra-color),
    0px 8px 10px 1px var(--jp-shadow-penumbra-color),
    0px 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0px 7px 8px -4px var(--jp-shadow-umbra-color),
    0px 12px 17px 2px var(--jp-shadow-penumbra-color),
    0px 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0px 8px 10px -5px var(--jp-shadow-umbra-color),
    0px 16px 24px 2px var(--jp-shadow-penumbra-color),
    0px 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0px 10px 13px -6px var(--jp-shadow-umbra-color),
    0px 20px 31px 3px var(--jp-shadow-penumbra-color),
    0px 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0px 11px 15px -7px var(--jp-shadow-umbra-color),
    0px 24px 38px 3px var(--jp-shadow-penumbra-color),
    0px 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;

  --jp-ui-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica,
    Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;

  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);

  --jp-content-link-color: var(--md-blue-700);

  --jp-content-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: Menlo, Consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-700);
  --jp-brand-color1: var(--md-blue-500);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);

  --jp-accent-color0: var(--md-green-700);
  --jp-accent-color1: var(--md-green-500);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-700);
  --jp-warn-color1: var(--md-orange-500);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);

  --jp-error-color0: var(--md-red-700);
  --jp-error-color1: var(--md-red-500);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);

  --jp-success-color0: var(--md-green-700);
  --jp-success-color1: var(--md-green-500);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);

  --jp-info-color0: var(--md-cyan-700);
  --jp-info-color1: var(--md-cyan-500);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;

  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;

  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);

  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: 'Source Code Pro', monospace;
  --jp-cell-prompt-letter-spacing: 0px;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);
  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;
  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0px 0px 2px 0px rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0px 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-border-color1);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: #05a;
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #aa22ff;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #aa22ff;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 180px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);
}
</style>

<style type="text/css">
a.anchor-link {
   display: none;
}
.highlight  {
    margin: 0.4em;
}

/* Input area styling */
.jp-InputArea {
    overflow: hidden;
}

.jp-InputArea-editor {
    overflow: hidden;
}

@media print {
  body {
    margin: 0;
  }
}
</style>



<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-MML-AM_CHTML-full,Safe"> </script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                CommonHTML: {
                    linebreaks: { 
                    automatic: true 
                    }
                },
                "HTML-CSS": {
                    linebreaks: { 
                    automatic: true 
                    }
                }
            });
        
            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
    <!-- End of mathjax configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">

<div class="jp-Cell-inputWrapper"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h1 id="Fusing-bayesian-optimization-explorations-at-different-sample-sizes">Fusing bayesian optimization explorations at different sample sizes<a class="anchor-link" href="#Fusing-bayesian-optimization-explorations-at-different-sample-sizes">&#182;</a></h1>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[22]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.datasets</span> <span class="kn">import</span> <span class="n">make_classification</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">cross_val_score</span>
<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">RandomForestClassifier</span> <span class="k">as</span> <span class="n">RFC</span>
<span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="kn">import</span> <span class="n">SVC</span>
<span class="kn">from</span> <span class="nn">sklearn.gaussian_process.kernels</span> <span class="kn">import</span> <span class="n">Matern</span><span class="p">,</span> <span class="n">WhiteKernel</span>
<span class="kn">from</span> <span class="nn">sklearn.gaussian_process</span> <span class="kn">import</span> <span class="n">GaussianProcessRegressor</span>
<span class="kn">from</span> <span class="nn">bayes_opt</span> <span class="kn">import</span> <span class="n">BayesianOptimization</span>
<span class="kn">from</span> <span class="nn">bayes_opt.util</span> <span class="kn">import</span> <span class="n">Colours</span>

<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">matplotlib</span> <span class="k">as</span> <span class="nn">mpl</span>
<span class="kn">from</span> <span class="nn">matplotlib</span> <span class="kn">import</span> <span class="n">colors</span><span class="p">,</span> <span class="n">cm</span> 

<span class="kn">from</span> <span class="nn">math</span> <span class="kn">import</span> <span class="n">log</span><span class="p">,</span> <span class="n">floor</span><span class="p">,</span> <span class="n">sqrt</span>

<span class="n">copper</span> <span class="o">=</span> <span class="n">mpl</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">copper</span> 
<span class="n">cNorm</span>  <span class="o">=</span> <span class="n">colors</span><span class="o">.</span><span class="n">Normalize</span><span class="p">(</span><span class="n">vmin</span><span class="o">=-</span><span class="mf">0.9</span><span class="p">,</span> <span class="n">vmax</span><span class="o">=-</span><span class="mf">0.25</span><span class="p">)</span>
<span class="n">scalarMap</span> <span class="o">=</span> <span class="n">cm</span><span class="o">.</span><span class="n">ScalarMappable</span><span class="p">(</span><span class="n">norm</span><span class="o">=</span><span class="n">cNorm</span><span class="p">,</span> <span class="n">cmap</span><span class="o">=</span><span class="n">copper</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Utilities to compute time allocation</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[23]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">cost_per_model</span><span class="p">(</span><span class="n">pct</span><span class="p">,</span> <span class="n">algo</span><span class="o">=</span><span class="s1">&#39;svm&#39;</span><span class="p">):</span> 
    <span class="n">x</span> <span class="o">=</span> <span class="p">[</span><span class="n">i</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">101</span><span class="p">,</span> <span class="mi">1</span><span class="p">)]</span> 
 
    <span class="k">if</span> <span class="n">algo</span> <span class="o">==</span> <span class="s1">&#39;rf&#39;</span><span class="p">:</span> 
        <span class="n">nlogn</span> <span class="o">=</span> <span class="p">[</span><span class="n">i</span><span class="o">*</span><span class="n">log</span><span class="p">(</span><span class="n">i</span><span class="p">)</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">x</span><span class="p">]</span>
        <span class="k">return</span> <span class="n">nlogn</span><span class="p">[</span><span class="mi">99</span><span class="p">]</span><span class="o">/</span><span class="n">nlogn</span><span class="p">[</span><span class="nb">int</span><span class="p">(</span><span class="n">pct</span><span class="o">*</span><span class="mi">100</span><span class="p">)</span> <span class="o">-</span> <span class="mi">1</span><span class="p">]</span>
    <span class="k">if</span> <span class="n">algo</span> <span class="o">==</span> <span class="s1">&#39;svm&#39;</span><span class="p">:</span>
        <span class="n">n_n</span> <span class="o">=</span> <span class="p">[</span><span class="n">i</span><span class="o">*</span><span class="n">i</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">x</span><span class="p">]</span>
        <span class="k">return</span> <span class="n">n_n</span><span class="p">[</span><span class="mi">99</span><span class="p">]</span><span class="o">/</span><span class="n">n_n</span><span class="p">[</span><span class="nb">int</span><span class="p">(</span><span class="n">pct</span><span class="o">*</span><span class="mi">100</span><span class="p">)</span> <span class="o">-</span> <span class="mi">1</span><span class="p">]</span> 
    


<span class="k">def</span> <span class="nf">budget_division</span><span class="p">(</span><span class="n">budget</span><span class="p">,</span> <span class="n">how</span><span class="o">=</span><span class="s1">&#39;equal&#39;</span><span class="p">,</span> <span class="n">steps</span><span class="o">=</span><span class="mi">3</span><span class="p">,</span> <span class="n">lower</span><span class="o">=</span><span class="mf">0.4</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">normalizing_factor</span><span class="p">(</span><span class="n">lst</span><span class="p">,</span> <span class="n">budget</span><span class="p">):</span>
        <span class="sd">&#39;&#39;&#39;sum(lst).X = budget&#39;&#39;&#39;</span>
        <span class="k">return</span> <span class="n">budget</span> <span class="o">/</span> <span class="nb">sum</span><span class="p">(</span><span class="n">lst</span><span class="p">)</span>
    
    <span class="k">if</span> <span class="n">how</span> <span class="o">==</span> <span class="s1">&#39;equal&#39;</span><span class="p">:</span>
        <span class="k">return</span> <span class="p">[</span><span class="nb">int</span><span class="p">(</span><span class="n">budget</span><span class="o">/</span><span class="n">steps</span><span class="p">)</span> <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">steps</span><span class="p">)]</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">slices</span> <span class="o">=</span> <span class="p">[</span><span class="n">budget</span><span class="o">/</span><span class="p">(</span><span class="mi">1</span><span class="o">+</span><span class="n">s</span><span class="p">)</span> <span class="k">for</span> <span class="n">s</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">steps</span><span class="p">)]</span>
        <span class="n">norm_factor</span> <span class="o">=</span> <span class="n">normalizing_factor</span><span class="p">(</span><span class="n">slices</span><span class="p">,</span> <span class="n">budget</span><span class="p">)</span>
        <span class="n">normalized_slices</span> <span class="o">=</span> <span class="p">[</span><span class="n">norm_factor</span><span class="o">*</span><span class="n">s</span> <span class="k">for</span> <span class="n">s</span> <span class="ow">in</span> <span class="n">slices</span><span class="p">]</span>
        
        <span class="k">if</span> <span class="n">how</span> <span class="o">==</span> <span class="s1">&#39;linear_asc&#39;</span><span class="p">:</span>
            <span class="k">return</span> <span class="n">normalized_slices</span>
        <span class="k">if</span> <span class="n">how</span> <span class="o">==</span> <span class="s1">&#39;linear_desc&#39;</span><span class="p">:</span>
            <span class="k">return</span> <span class="n">normalized_slices</span><span class="p">[::</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
        

<span class="k">def</span> <span class="nf">models_at_sample_size</span><span class="p">(</span><span class="n">budget</span><span class="p">,</span> <span class="n">sample_size</span><span class="p">,</span> <span class="n">algo</span><span class="p">):</span>
    <span class="k">return</span> <span class="nb">int</span><span class="p">(</span><span class="n">budget</span><span class="o">*</span><span class="n">cost_per_model</span><span class="p">(</span><span class="n">sample_size</span><span class="p">,</span> <span class="n">algo</span><span class="p">))</span>


<span class="k">def</span> <span class="nf">size</span><span class="p">(</span><span class="n">i</span><span class="p">,</span> <span class="n">lower</span><span class="o">=</span><span class="mf">0.4</span><span class="p">,</span> <span class="n">steps</span><span class="o">=</span><span class="mi">3</span><span class="p">):</span>
    <span class="c1">#i += 1</span>
    <span class="k">return</span> <span class="n">lower</span> <span class="o">+</span> <span class="n">i</span> <span class="o">*</span> <span class="p">(</span><span class="mi">1</span> <span class="o">-</span> <span class="n">lower</span><span class="p">)</span><span class="o">/</span><span class="p">(</span><span class="n">steps</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Data generation</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[24]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">get_data</span><span class="p">():</span>
    <span class="sd">&quot;&quot;&quot;Synthetic binary classification dataset.&quot;&quot;&quot;</span>
    <span class="n">data</span><span class="p">,</span> <span class="n">targets</span> <span class="o">=</span> <span class="n">make_classification</span><span class="p">(</span>
        <span class="n">n_samples</span><span class="o">=</span><span class="mi">5_000</span><span class="p">,</span>
        <span class="n">n_features</span><span class="o">=</span><span class="mi">22</span><span class="p">,</span>
        <span class="n">n_informative</span><span class="o">=</span><span class="mi">12</span><span class="p">,</span>
        <span class="n">n_redundant</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> 
        <span class="n">random_state</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span>
    <span class="p">)</span>
    <span class="k">return</span> <span class="n">data</span><span class="p">,</span> <span class="n">targets</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div>
<div class="jp-Cell-inputWrapper"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<p>Function to optimize: random forest classifier being score with negative log loss.</p>

</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[25]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">rfc_cv</span><span class="p">(</span><span class="n">n_estimators</span><span class="p">,</span> <span class="n">min_samples_split</span><span class="p">,</span> <span class="n">max_features</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span> <span class="n">targets</span><span class="p">):</span> 
    <span class="n">estimator</span> <span class="o">=</span> <span class="n">RFC</span><span class="p">(</span>
        <span class="n">n_estimators</span><span class="o">=</span><span class="n">n_estimators</span><span class="p">,</span>
        <span class="n">min_samples_split</span><span class="o">=</span><span class="n">min_samples_split</span><span class="p">,</span>
        <span class="n">max_features</span><span class="o">=</span><span class="n">max_features</span><span class="p">,</span>
        <span class="n">random_state</span><span class="o">=</span><span class="mi">2</span>
    <span class="p">)</span> 
    
    <span class="n">cval</span> <span class="o">=</span> <span class="n">cross_val_score</span><span class="p">(</span><span class="n">estimator</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span> <span class="n">targets</span><span class="p">,</span>
                           <span class="n">scoring</span><span class="o">=</span><span class="s1">&#39;neg_log_loss&#39;</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">cval</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
 
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[51]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># points to probe in next level. </span>
<span class="c1"># Something dynamic like sqrt(observations) could do the job but needs additional control mechanisms.</span>
<span class="n">n_points</span> <span class="o">=</span> <span class="mi">5</span>

<span class="kn">from</span> <span class="nn">sklearn.gaussian_process.kernels</span> <span class="kn">import</span> <span class="p">(</span><span class="n">RBF</span><span class="p">,</span> <span class="n">Matern</span><span class="p">,</span> <span class="n">RationalQuadratic</span><span class="p">,</span>
                                              <span class="n">ExpSineSquared</span><span class="p">,</span> <span class="n">DotProduct</span><span class="p">,</span>
                                              <span class="n">ConstantKernel</span><span class="p">)</span>
<span class="k">def</span> <span class="nf">points_to_probe</span><span class="p">(</span><span class="n">optimizer</span><span class="p">):</span>
    <span class="n">x0_obs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([[</span><span class="n">res</span><span class="p">[</span><span class="s2">&quot;params&quot;</span><span class="p">][</span><span class="s2">&quot;max_features&quot;</span><span class="p">]]</span> <span class="k">for</span> <span class="n">res</span> <span class="ow">in</span> <span class="n">optimizer</span><span class="o">.</span><span class="n">res</span><span class="p">])</span> 
    <span class="n">x1_obs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([[</span><span class="n">res</span><span class="p">[</span><span class="s2">&quot;params&quot;</span><span class="p">][</span><span class="s2">&quot;min_samples_split&quot;</span><span class="p">]]</span> <span class="k">for</span> <span class="n">res</span> <span class="ow">in</span> <span class="n">optimizer</span><span class="o">.</span><span class="n">res</span><span class="p">])</span>
    <span class="n">x2_obs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([[</span><span class="n">res</span><span class="p">[</span><span class="s2">&quot;params&quot;</span><span class="p">][</span><span class="s2">&quot;n_estimators&quot;</span><span class="p">]]</span> <span class="k">for</span> <span class="n">res</span> <span class="ow">in</span> <span class="n">optimizer</span><span class="o">.</span><span class="n">res</span><span class="p">])</span> 
    <span class="n">y_obs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">res</span><span class="p">[</span><span class="s2">&quot;target&quot;</span><span class="p">]</span> <span class="k">for</span> <span class="n">res</span> <span class="ow">in</span> <span class="n">optimizer</span><span class="o">.</span><span class="n">res</span><span class="p">])</span> 
     

    <span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span><span class="mi">6</span><span class="p">))</span>
    <span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">111</span><span class="p">,</span> <span class="n">projection</span><span class="o">=</span><span class="s1">&#39;3d&#39;</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">m</span><span class="p">,</span> <span class="n">zlow</span><span class="p">,</span> <span class="n">zhigh</span> <span class="ow">in</span> <span class="p">[(</span><span class="s1">&#39;o&#39;</span><span class="p">,</span> <span class="o">-</span><span class="mi">50</span><span class="p">,</span> <span class="o">-</span><span class="mi">25</span><span class="p">),</span> <span class="p">(</span><span class="s1">&#39;^&#39;</span><span class="p">,</span> <span class="o">-</span><span class="mi">30</span><span class="p">,</span> <span class="o">-</span><span class="mi">5</span><span class="p">)]:</span> 
        <span class="n">ax</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x0_obs</span><span class="p">,</span> <span class="n">x1_obs</span><span class="p">,</span> <span class="n">x2_obs</span><span class="p">,</span> <span class="n">c</span><span class="o">=</span><span class="n">scalarMap</span><span class="o">.</span><span class="n">to_rgba</span><span class="p">(</span><span class="n">y_obs</span><span class="p">),</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">)</span>

    <span class="n">ax</span><span class="o">.</span><span class="n">set_xlabel</span><span class="p">(</span><span class="s1">&#39;max_features&#39;</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_ylabel</span><span class="p">(</span><span class="s1">&#39;min_samples_split&#39;</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_zlabel</span><span class="p">(</span><span class="s1">&#39;n_estimators&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">colorbar</span><span class="p">(</span><span class="n">scalarMap</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">tight_layout</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
        
    <span class="c1">#plt.matshow(optimizer._gp.L_)</span>
    <span class="c1">#plt.title(&#39;Lower-triangular Cholesky decomposition of cov&#39;)</span>
    <span class="c1">#plt.show() </span>
    
    <span class="n">idx</span> <span class="o">=</span> <span class="n">y_obs</span><span class="o">.</span><span class="n">argsort</span><span class="p">()[</span><span class="o">-</span><span class="n">n_points</span><span class="p">:][::</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
    <span class="n">probe</span> <span class="o">=</span> <span class="p">[[</span><span class="n">x0_obs</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">x1_obs</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">x2_obs</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">idx</span><span class="p">]</span>
    
    <span class="k">return</span> <span class="n">probe</span>



<span class="k">def</span> <span class="nf">optimize_rfc</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">targets</span><span class="p">,</span> <span class="n">level</span><span class="p">,</span> <span class="n">cov_function_prior</span><span class="p">,</span> <span class="n">n_iter</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> <span class="n">bounds</span><span class="o">=</span><span class="kc">None</span><span class="p">,</span> <span class="n">to_probe</span><span class="o">=</span><span class="kc">None</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    level: index + 1 of sample size in [pct0, pct1, .. pctN].</span>
<span class="sd">    cov_function_prior: definition of cov. function by the gaussian process regression. It&#39;s going to be updated every step.</span>
<span class="sd">    n_iter: number of models to be computed at each sample size. Is constrained by the total budget.</span>
<span class="sd">    bounds: updated boundaries for hyper param. space.</span>
<span class="sd">    to_probe: promissing points found in smaller sample sizes.</span>
<span class="sd">    </span>
<span class="sd">    </span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="k">def</span> <span class="nf">rfc_crossval</span><span class="p">(</span><span class="n">n_estimators</span><span class="p">,</span> <span class="n">min_samples_split</span><span class="p">,</span> <span class="n">max_features</span><span class="p">):</span> 
        <span class="k">return</span> <span class="n">rfc_cv</span><span class="p">(</span>
            <span class="n">n_estimators</span><span class="o">=</span><span class="nb">int</span><span class="p">(</span><span class="n">n_estimators</span><span class="p">),</span>
            <span class="n">min_samples_split</span><span class="o">=</span><span class="nb">float</span><span class="p">(</span><span class="n">min_samples_split</span><span class="p">),</span>
            <span class="n">max_features</span><span class="o">=</span><span class="nb">max</span><span class="p">(</span><span class="nb">min</span><span class="p">(</span><span class="n">max_features</span><span class="p">,</span> <span class="mf">0.999</span><span class="p">),</span> <span class="mf">1e-3</span><span class="p">),</span> 
            <span class="n">data</span><span class="o">=</span><span class="n">data</span><span class="p">,</span>
            <span class="n">targets</span><span class="o">=</span><span class="n">targets</span><span class="p">,</span>
        <span class="p">)</span>

    <span class="n">optimizer</span> <span class="o">=</span> <span class="n">BayesianOptimization</span><span class="p">(</span>
        <span class="n">f</span><span class="o">=</span><span class="n">rfc_crossval</span><span class="p">,</span>
        <span class="n">pbounds</span><span class="o">=</span><span class="p">{</span>
            <span class="s2">&quot;n_estimators&quot;</span><span class="p">:</span> <span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">250</span><span class="p">),</span>
            <span class="s2">&quot;min_samples_split&quot;</span><span class="p">:</span> <span class="p">(</span><span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.999</span><span class="p">),</span>
            <span class="s2">&quot;max_features&quot;</span><span class="p">:</span> <span class="p">(</span><span class="mf">0.1</span><span class="p">,</span> <span class="mf">0.999</span><span class="p">),</span> 
        <span class="p">},</span>
        <span class="n">random_state</span><span class="o">=</span><span class="mi">1234</span><span class="p">,</span>
        <span class="n">verbose</span><span class="o">=</span><span class="mi">1</span>
    <span class="p">)</span> 
    
    <span class="c1"># model noise in each sample size (level)</span>
    <span class="n">optimizer</span><span class="o">.</span><span class="n">_gp</span><span class="o">.</span><span class="n">kernel</span> <span class="o">=</span> <span class="n">cov_function_prior</span> <span class="o">+</span> <span class="n">WhiteKernel</span><span class="p">(</span><span class="n">noise_level</span><span class="o">=</span><span class="mf">0.01</span><span class="o">/</span><span class="p">(</span><span class="n">level</span> <span class="o">+</span> <span class="mi">1</span><span class="p">))</span>
     
    <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">to_probe</span><span class="p">)</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">:</span>
        <span class="k">for</span> <span class="n">point</span> <span class="ow">in</span> <span class="n">to_probe</span><span class="p">:</span> 
            <span class="n">optimizer</span><span class="o">.</span><span class="n">probe</span><span class="p">(</span>
                <span class="n">params</span><span class="o">=</span><span class="n">point</span><span class="p">,</span>
                <span class="n">lazy</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span>
                <span class="p">)</span>
    
    <span class="c1"># control structure to constrain compute budget</span>
    <span class="k">if</span> <span class="n">level</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span>
        <span class="n">init_points</span> <span class="o">=</span> <span class="mi">2</span> <span class="c1"># minimum amount of points to start inference -&gt; randomly generated.</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">init_points</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">n_iter</span> <span class="o">-=</span> <span class="n">n_points</span> 
        
    <span class="n">optimizer</span><span class="o">.</span><span class="n">maximize</span><span class="p">(</span><span class="n">init_points</span><span class="o">=</span><span class="n">init_points</span><span class="p">,</span> <span class="n">n_iter</span><span class="o">=</span><span class="n">n_iter</span><span class="p">,</span> <span class="n">acq</span><span class="o">=</span><span class="s2">&quot;ucb&quot;</span><span class="p">,</span> <span class="n">kappa</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span> 
    
    <span class="c1">#print(Colours.yellow(f&#39;Prior kernel: {optimizer._gp.kernel}&#39;))</span>
    <span class="c1">#print(Colours.purple(f&#39;Posterior kernel: {optimizer._gp.kernel_}&#39;))</span>
    
    <span class="n">cov_function_posterior</span> <span class="o">=</span> <span class="n">optimizer</span><span class="o">.</span><span class="n">_gp</span><span class="o">.</span><span class="n">kernel_</span>

    <span class="k">return</span> <span class="n">points_to_probe</span><span class="p">(</span><span class="n">optimizer</span><span class="p">),</span> <span class="n">cov_function_posterior</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[52]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">data</span><span class="p">,</span> <span class="n">targets</span> <span class="o">=</span> <span class="n">get_data</span><span class="p">()</span>

<span class="n">lower</span> <span class="o">=</span> <span class="mi">1</span>
<span class="n">steps</span> <span class="o">=</span> <span class="mi">2</span>
<span class="n">budget</span> <span class="o">=</span> <span class="mi">200</span>

<span class="n">bounds</span> <span class="o">=</span> <span class="kc">None</span>
<span class="n">to_probe</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">cov_function_prior</span> <span class="o">=</span> <span class="n">Matern</span><span class="p">(</span><span class="n">nu</span><span class="o">=</span><span class="mf">2.5</span><span class="p">)</span> <span class="o">+</span> <span class="n">WhiteKernel</span><span class="p">(</span><span class="n">noise_level</span><span class="o">=</span><span class="mf">0.01</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="k">for</span> <span class="n">level</span><span class="p">,</span> <span class="n">b</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">budget_division</span><span class="p">(</span><span class="n">budget</span><span class="p">,</span> <span class="n">how</span><span class="o">=</span><span class="s1">&#39;equal&#39;</span><span class="p">,</span> <span class="n">steps</span><span class="o">=</span><span class="n">steps</span><span class="p">,</span> <span class="n">lower</span><span class="o">=</span><span class="n">lower</span><span class="p">)):</span>
    <span class="n">sample_size</span> <span class="o">=</span> <span class="n">size</span><span class="p">(</span><span class="n">level</span><span class="p">,</span> <span class="n">lower</span><span class="p">,</span> <span class="n">steps</span><span class="p">)</span> 
    <span class="n">n_iter</span> <span class="o">=</span> <span class="n">models_at_sample_size</span><span class="p">(</span><span class="n">b</span><span class="p">,</span> <span class="n">sample_size</span><span class="p">,</span> <span class="s1">&#39;rf&#39;</span><span class="p">)</span>
    
    <span class="n">rows</span> <span class="o">=</span> <span class="nb">int</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">data</span><span class="p">)</span> <span class="o">*</span> <span class="n">sample_size</span><span class="p">)</span>
    <span class="n">idx</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">data</span><span class="p">),</span> <span class="n">rows</span><span class="p">,</span> <span class="n">replace</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
    <span class="n">sampled_X</span> <span class="o">=</span> <span class="n">data</span><span class="p">[</span><span class="n">idx</span><span class="p">,:]</span>
    <span class="n">sampled_y</span> <span class="o">=</span> <span class="n">targets</span><span class="p">[</span><span class="n">idx</span><span class="p">]</span>

    <span class="nb">print</span><span class="p">(</span><span class="n">Colours</span><span class="o">.</span><span class="n">green</span><span class="p">(</span><span class="sa">f</span><span class="s2">&quot;--- Optimizing Random Forest: </span><span class="si">{</span><span class="n">n_iter</span><span class="si">}</span><span class="s2"> models; budget: </span><span class="si">{</span><span class="n">b</span><span class="si">}</span><span class="s2"> --- &quot;</span><span class="p">))</span>
    <span class="n">to_probe</span><span class="p">,</span> <span class="n">cov_function_posterior</span> <span class="o">=</span> <span class="n">optimize_rfc</span><span class="p">(</span><span class="n">sampled_X</span><span class="p">,</span> <span class="n">sampled_y</span><span class="p">,</span> <span class="n">level</span> <span class="o">+</span> <span class="mi">1</span><span class="p">,</span> <span class="n">cov_function_prior</span><span class="p">,</span> <span class="n">n_iter</span><span class="p">,</span> <span class="n">bounds</span><span class="p">,</span> <span class="n">to_probe</span><span class="p">)</span>
    
    <span class="n">cov_function_prior</span> <span class="o">=</span> <span class="n">cov_function_posterior</span> 
     
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">
<pre><span class="ansi-green-intense-fg">--- Optimizing Random Forest: 100 models; budget: 100 --- </span>
|   iter    |  target   | max_fe... | min_sa... | n_esti... |
-------------------------------------------------------------
| <span class="ansi-magenta-intense-fg"> 4       </span> | <span class="ansi-magenta-intense-fg">-0.3423  </span> | <span class="ansi-magenta-intense-fg"> 0.4902  </span> | <span class="ansi-magenta-intense-fg"> 0.02077 </span> | <span class="ansi-magenta-intense-fg"> 10.02   </span> |
| <span class="ansi-magenta-intense-fg"> 5       </span> | <span class="ansi-magenta-intense-fg">-0.3404  </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 10.0    </span> |
| <span class="ansi-magenta-intense-fg"> 6       </span> | <span class="ansi-magenta-intense-fg">-0.3149  </span> | <span class="ansi-magenta-intense-fg"> 0.9771  </span> | <span class="ansi-magenta-intense-fg"> 0.01587 </span> | <span class="ansi-magenta-intense-fg"> 188.5   </span> |
| <span class="ansi-magenta-intense-fg"> 12      </span> | <span class="ansi-magenta-intense-fg">-0.2959  </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 96.31   </span> |
| <span class="ansi-magenta-intense-fg"> 16      </span> | <span class="ansi-magenta-intense-fg">-0.2946  </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 141.4   </span> |
| <span class="ansi-magenta-intense-fg"> 51      </span> | <span class="ansi-magenta-intense-fg">-0.2943  </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 122.7   </span> |
| <span class="ansi-magenta-intense-fg"> 95      </span> | <span class="ansi-magenta-intense-fg">-0.2942  </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 126.5   </span> |
=============================================================
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedText jp-OutputArea-output " data-mime-type="text/plain">
<pre>&lt;Figure size 432x288 with 0 Axes&gt;</pre>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">
<pre><span class="ansi-green-intense-fg">--- Optimizing Random Forest: 100 models; budget: 100 --- </span>
|   iter    |  target   | max_fe... | min_sa... | n_esti... |
-------------------------------------------------------------
| <span class="ansi-magenta-intense-fg"> 2       </span> | <span class="ansi-magenta-intense-fg">-0.2939  </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 122.7   </span> |
| <span class="ansi-magenta-intense-fg"> 3       </span> | <span class="ansi-magenta-intense-fg">-0.2935  </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 141.4   </span> |
| <span class="ansi-magenta-intense-fg"> 4       </span> | <span class="ansi-magenta-intense-fg">-0.2931  </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 208.6   </span> |
| <span class="ansi-magenta-intense-fg"> 54      </span> | <span class="ansi-magenta-intense-fg">-0.293   </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 189.1   </span> |
| <span class="ansi-magenta-intense-fg"> 89      </span> | <span class="ansi-magenta-intense-fg">-0.293   </span> | <span class="ansi-magenta-intense-fg"> 0.999   </span> | <span class="ansi-magenta-intense-fg"> 0.01    </span> | <span class="ansi-magenta-intense-fg"> 192.9   </span> |
=============================================================
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>

</div>

</div>
</body>







</html>
