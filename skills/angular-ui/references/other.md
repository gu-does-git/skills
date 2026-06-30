# Angular-Ui - Other

**Pages:** 1

---

## Angular directives for Bootstrap

**URL:** https://angular-ui.github.io/bootstrap/versioned-docs/1.1.2/

**Contents:**

- UI Bootstrap
- Getting started
  - Dependencies
  - Files to download
  - Installation
  - Migration to prefixes
  - CSS
  - FAQ
  - Reading the documentation
- Accordion (ui.bootstrap.accordion)

Bootstrap components written in pure AngularJS by the AngularUI Team

Code on Github Download (1.1.2) Create a Build

This repository contains a set of native AngularJS directives based on Bootstrap's markup and CSS. As a result no dependency on jQuery or Bootstrap's JavaScript is required. The only required dependencies are:

Build files for all directives are distributed in several flavours: minified for production usage, un-minified for development, with or without templates. All the options are described and can be downloaded from here. It should be noted that the -tpls files contain the templates bundled in JavaScript, while the regular version does not contain the bundled templates. For more information, check out the FAQ here and the README here.

Alternativelly, if you are only interested in a subset of directives, you can create your own build.

Whichever method you choose the good news that the overall size of a download is very small: <76kB for all directives (~20kB with gzip compression!)

As soon as you've got all the files downloaded and included in your page you just need to declare a dependency on the ui.bootstrap module: angular.module('myModule', ['ui.bootstrap']);

You can fork one of the plunkers from this page to see a working example of what is described here.

Since version 0.14.0 we started to prefix all our components. If you are upgrading from ui-bootstrap 0.13.4 or earlier, check our migration guide.

Original Bootstrap's CSS depends on empty href attributes to style cursors for several components (pagination, tabs etc.). But in AngularJS adding empty href attributes to link tags will cause unwanted route changes. This is why we need to remove empty href attributes from directive templates and as a result styling is not applied correctly. The remedy is simple, just add the following styling to your application: .nav, .pagination, .carousel, .panel-title a { cursor: pointer; }

Please check our FAQ section for common problems / solutions.

Each of the components provided in ui-bootstrap have documentation and interactive Plunker examples.

For the directives, we list the different attributes with their default values. In addition to this, some settings have a badge on it: - This setting has an angular $watch listener applied to it. B - This setting is a boolean. It doesn't need a parameter. C - This setting can be configured globally in a constant service\*. $ - This setting expects an angular expression instead of a literal string. If the expression support a boolean / integer, you can pass it directly. readonly - This setting is readonly.

For the services (you will recognize them with the $ prefix), we list all the possible parameters you can pass to them and their default values if any.

- Some directives have a config service that follows the next pattern: uibDirectiveConfig. The service's settings use camel case. The services can be configured in a .config function for example.

Toggle last panel Enable / Disable first panel

The body of the uib-accordion group grows to fit the contents

Please, to delete your account, click the button below

The accordion directive builds on top of the collapse directive to provide a list of items, with collapsible bodies that are collapsed or expanded by clicking on the item's header.

The body of each accordion group is transcluded into the body of the collapsible element.

close-others $ C (Default: true) - Control whether expanding an item will cause the other items to close.

template-url (Default: template/accordion/accordion.html) - Add the ability to override the template used on the component.

heading (Default: none) - The clickable text on the group's header. You need one to be able to click on the header for toggling.

is-disabled $ (Default: false) - Whether the accordion group is disabled or not.

is-open $ (Default: false) - Whether accordion group is open or closed.

panel-class (Default: panel-default) - Add ability to use Bootstrap's contextual panel classes (panel-primary, panel-success, panel-info, etc...) or your own. This must be a string.

template-url (Default: uib/template/accordion/accordion-group.html) - Add the ability to override the template used on the component.

Instead of the heading attribute on the uib-accordion-group, you can use an uib-accordion-heading element inside a group that will be used as the group's header.

To use clickable elements within the accordion, you have override the accordion-group template to use div elements instead of anchor elements, and add cursor: pointer in your CSS. This is due to browsers interpreting anchor elements as the target of any click event, which triggers routing when certain elements such as buttons are nested inside the anchor element.

If custom classes on the accordion-group element are desired, one needs to either modify the template to remove the ng-class usage in the accordion-group template and use ng-class on the accordion-group element (not recommended), or use an interpolated expression in the class attribute, i.e. <uib-accordion-group class="{{customClass()}}"></uib-accordion-group>.

This directive can be used both to generate alerts from static and dynamic model data (using the ng-repeat directive).

close() $ - A callback function that gets fired when an alert is closed. If the attribute exists, a close button is displayed as well.

dismiss-on-timeout (Default: none) - Takes the number of milliseconds that specify the timeout duration, after which the alert will be closed. This attribute requires the presence of the close attribute.

template-url (Default: uib/template/alert/alert.html) - Add the ability to override the template used in the component.

type (Default: warning) - Defines the type of the alert. Go to bootstrap page to see the type of alerts available.

With the buttons directive, we can make a group of buttons behave like a set of checkboxes (uib-btn-checkbox) or behave like a set of radio buttons (uib-btn-radio).

btn-checkbox-false (Default: false) - Sets the value for the unchecked status.

btn-checkbox-true (Default: true) - Sets the value for the checked status.

ng-model $ - Model where we set the checkbox status. By default true or false.

ng-model $ - Model where we set the radio status. All radio buttons in a group should use the same ng-model.

uib-btn-radio - $ Value to assign to the ng-model if we check this radio button.

uib-uncheckable $ (Default: null) - An expression that evaluates to a truthy or falsy value that determines whether the uncheckable attribute is present.

uncheckable B - Whether a radio button can be unchecked or not.

activeClass (Default: active) - Class to apply to the checked buttons.

toggleEvent (Default: click) - Event used to toggle the buttons.

Carousel creates a carousel similar to bootstrap's image carousel.

The carousel also offers support for touchscreen devices in the form of swiping. To enable swiping, load the ngTouch module as a dependency.

Use a <uib-carousel> element with <uib-slide> elements inside it.

interval $ (Default: none) - Sets an interval to cycle through the slides. You need a number bigger than 0 to make the interval work.

no-pause $ (Default: false) - The interval pauses on mouseover. Setting this to truthy, disables this pause.

no-transition $ (Default: false) - Whether to disable the transition animation between slides. Setting this to truthy, disables this transition.

no-wrap $ (Default: false) - Disables the looping of slides. Setting no-wrap to an expression which evaluates to a truthy value will prevent looping.

template-url (Default: uib/template/carousel/carousel.html) - Add the ability to override the template used on the component.

active $ (Default: false) - Sets the slide as the active one.

actual $ (Default: none) - Use this attribute to bind the slide model (or any object of interest) onto the slide scope, which makes it available for customization in the carousel template.

index $ (Default: none) - Use this attribute to change how the slides are ordered.

template-url (Default: uib/template/carousel/slide.html) - Add the ability to override the template used on the component.

uib-collapse provides a simple way to hide and show an element with a css transition

collapsed() $ - An optional expression called after the element finished collapsing.

collapsing() $ - An optional expression called before the element begins collapsing. If the expression returns a promise, animation won't start until the promise resolves. If the returned promise is rejected, collapsing will be cancelled.

expanded() $ - An optional expression called after the element finished expanding.

expanding() $ - An optional expression called before the element begins expanding. If the expression returns a promise, animation won't start until the promise resolves. If the returned promise is rejected, expanding will be cancelled.

uib-collapse $ (Default: false) - Whether the element should be collapsed or not.

The uibDateParser is what the uib-datepicker uses internally to parse the dates. You can use it standalone by injecting the uibDateParser service where you need it.

The public API for the dateParser is a single method called parse.

Certain format codes support i18n. Check this guide for more information.

input (Type: string, Example: 2004/Sep/4) - The input date to parse.

format (Type: string, Example: yyyy/MMM/d) - The format we want to use. Check all the supported formats below.

baseDate (Type: Date, Example: new Date()) - If you want to parse a date but maintain the timezone, you can pass an existing date here.

yyyy (Example: 2015) - Parses a 4 digits year.

yy (Example: 15) - Parses a 2 digits year.

y (Example: 15) - Parses a year with 1, 2, 3, or 4 digits.

MMMM (Example: February, i18n support) - Parses the full name of a month.

MMM (Example: Feb, i18n support) - Parses the short name of a month.

MM (Example: 12, Leading 0) - Parses a numeric month.

M (Example: 3) - Parses a numeric month.

M! (Example: 3 or 03) - Parses a numeric month, but allowing an optional leading zero

dd (Example: 05, Leading 0) - Parses a numeric day.

d (Example: 5) - Parses a numeric day.

d! (Example: 3 or 03) - Parses a numeric day, but allowing an optional leading zero

EEEE (Example: Sunday, i18n support) - Parses the full name of a day.

EEE (Example: Mon, i18n support) - Parses the short name of a day.

HH (Example: 14, Leading 0) - Parses a 24 hours time.

H (Example: 3) - Parses a 24 hours time.

hh (Example: 11, Leading 0) - Parses a 12 hours time.

h (Example: 3) - Parses a 12 hours time.

mm (Example: 09, Leading 0) - Parses the minutes.

m (Example: 3) - Parses the minutes.

sss (Example: 094, Leading 0) - Parses the milliseconds.

ss (Example: 08, Leading 0) - Parses the seconds.

s (Example: 22) - Parses the seconds.

a (Example: 10AM) - Parses a 12 hours time with AM/PM.

Z (Example: -0800) - Parses the timezone offset in a signed 4 digit representation

ww (Example: 03, Leading 0) - Parses the week number

w (Example: 03) - Parses the week number

G, GG, GGG (Example: AD) - Parses the era (AD or BC)

- The ones marked with Leading 0, needs a leading 0 for values less than 10. Exception being milliseconds which needs it for values under 100.

\*\* It also supports fullDate|longDate|medium|mediumDate|mediumTime|short|shortDate|shortTime as the format for parsing.

\*\*\* It supports template literals as a string between the single quote ' character, i.e. 'The Date is' MM/DD/YYYY. If one wants the literal single quote character, one must use ''''.

Our datepicker is flexible and fully customizable.

You can navigate through days, months and years.

It comes in two formats, an inline uib-datepicker and an uib-datepicker-popup to be embedded in an input.

The datepicker has 3 modes:

custom-class (date, mode) $ - An optional expression to add classes based on passing a date and current mode.

date-disabled (date, mode) $ - An optional expression to disable visible options based on passing a date and current mode.

datepicker-mode $ C (Default: day) - Current mode of the datepicker (day|month|year). Can be used to initialize the datepicker in a specific mode.

datepicker-options $ - An optional object to configure the datepicker in one place. If this attribute is used, all supported options must be specified instead of the attributes.

The supported options are:

format-day C (Default: dd) - Format of day in month.

format-month C (Default: MMMM) - Format of month in year.

format-year C (Default: yyyy) - Format of year in year range.

format-day-header C (Default: EEE) - Format of day in week header.

format-day-title C (Default: MMMM yyyy) - Format of title when selecting day.

format-month-title C (Default: yyyy) - Format of title when selecting month.

init-date $ (Default: null) - The initial date view when no model value is specified.

max-date $ C (Default: null) - Defines the maximum available date.

max-mode $ C (Default: year) - Sets an upper limit for mode.

min-date $ C (Default: null) - Defines the minimum available date.

min-mode $ C (Default: day) - Sets a lower limit for mode.

ng-model $ - The date object. Needs to be a Javascript Date object.

ng-model-options $ C (Default: {}) - Supported properties:

shortcut-propagation $ C (Default: false) - An option to disable the propagation of the keydown event.

show-weeks $ C (Default: true) - Whether to display week numbers.

starting-day $ C (Default: $locale.DATETIME_FORMATS.FIRSTDAYOFWEEK) - Starting day of the week from 0-6 (0=Sunday, ..., 6=Saturday).

template-url (Default: uib/template/datepicker/datepicker.html) - Add the ability to override the template used on the component.

year-rows $ C (Default: 4) - Number of rows displayed in year selection.

year-columns $ C (Default: 5) - Number of columns displayed in year selection.

The popup is a wrapper that you can use in an input to toggle a datepicker. To configure the datepicker, use datepicker-options.

alt-input-formats $ C (Default: []) - A list of alternate formats acceptable for manual entry.

clear-text C (Default: Clear) - The text to display for the clear button.

close-on-date-selection $ C (Default: true) - Whether to close calendar when a date is chosen.

close-text C (Default: Done) - The text to display for the close button.

current-text C (Default: Today) - The text to display for the current day button.

datepicker-append-to-body $ C (Default: false, Config: appendToBody) - Append the datepicker popup element to body, rather than inserting after datepicker-popup.

datepicker-options $ - An object with any combination of the datepicker settings (in camelCase) used to configure the wrapped datepicker.

datepicker-popup-template-url C (Default: uib/template/datepicker/popup.html) - Add the ability to override the template used on the component.

datepicker-template-url C (Default: uib/template/datepicker/datepicker.html) - Add the ability to override the template used on the component (inner uib-datepicker).

is-open $ (Default: false) - Whether or not to show the datepicker.

on-open-focus $ C (Default: true) - Whether or not to focus the datepicker popup upon opening.

show-button-bar $ C (Default: true) - Whether or not to display a button bar underneath the uib-datepicker.

type C (Default: text, Config: html5Types) - You can override the input type to be (date|datetime-local|month). That will change the date format of the popup.

uib-datepicker-popup C (Default: yyyy-MM-dd, Config: datepickerConfig) - The format for displayed dates. This string can take string literals by surrounding the value with single quotes, i.e. yyyy-MM-dd h 'o\'clock'.

Note: With the exception of ng-model[-options] and templateUrl, you can configure the wrapped datepicker using its attributes in the popup as well. But beware this possibility may be deprecated on the near future.

Depending on datepicker's current mode, the date may refer either to day, month or year. Accordingly, the term view refers either to a month, year or year range.

If the date a user enters falls outside of the min-/max-date range, a dateDisabled validation error will show on the form.

If using this directive on input type date, a native browser datepicker could also appear.

Toggle button dropdown Enable/Disable

Dropdown is a simple directive which will toggle a dropdown menu on click or programmatically.

This directive is composed by three parts:

Each of these parts need to be used as attribute directives.

auto-close (Default: always) - Controls the behavior of the menu when clicked.

dropdown-append-to $ (Default: null) - Appends the inner dropdown-menu to an arbitrary DOM element.

dropdown-append-to-body B (Default: false) - Appends the inner dropdown-menu to the body element.

is-open $ (Default: false) - Defines whether or not the dropdown-menu is open. The uib-dropdown-toggle will toggle this attribute on click.

keyboard-nav: B (Default: false) - Enables navigation of dropdown list elements with the arrow keys.

on-toggle(open) $ - An optional expression called when the dropdown menu is opened or closed.

appendToOpenClass (Default: uib-dropdown-open) - Class to apply when the dropdown is open and appended to a different DOM element.

openClass (Default: open) - Class to apply when the dropdown is open.

For usage with ngTouch, it is recommended to use the programmatic is-open trigger with ng-click - this is due to ngTouch decorating ng-click to prevent propagation of the event.

$uibModal is a service to create modal windows. Creating modals is straightforward: create a template, a controller and reference them when using $uibModal.

The $uibModal service has only one method: open(options).

animation (Type: boolean, Default: true) - Set to false to disable animations on new modal/backdrop. Does not toggle animations for modals/backdrops that are already displayed.

appendTo (Type: angular.element, Default: body: Example: $document.find('aside').eq(0)) - Appends the modal to a specific element.

backdrop (Type: boolean|string, Default: true) - Controls presence of a backdrop. Allowed values: true (default), false (no backdrop), 'static' (disables modal closing by click on the backdrop).

backdropClass (Type: string) - Additional CSS class(es) to be added to a modal backdrop template.

bindToController (Type: boolean, Default: false) - When used with controllerAs & set to true, it will bind the $scope properties onto the controller.

controller (Type: function|string|array, Example: MyModalController) - A controller for the modal instance, either a controller name as a string, or an inline controller function, optionally wrapped in array notation for dependency injection. Allows the controller-as syntax. Has a special $uibModalInstance injectable to access the modal instance.

controllerAs (Type: string, Example: ctrl) - An alternative to the controller-as syntax. Requires the controller option to be provided as well.

keyboard - (Type: boolean, Default: true) - Indicates whether the dialog should be closable by hitting the ESC key.

openedClass (Type: string, Default: modal-open) - Class added to the body element when the modal is opened.

resolve (Type: Object) - Members that will be resolved and passed to the controller as locals; it is equivalent of the resolve property in the router.

scope (Type: $scope) - The parent scope instance to be used for the modal's content. Defaults to $rootScope.

size (Type: string, Example: lg) - Optional suffix of modal window class. The value used is appended to the modal- class, i.e. a value of sm gives modal-sm.

template (Type: string) - Inline template representing the modal's content.

templateUrl (Type: string) - A path to a template representing modal's content. You need either a template or templateUrl.

windowClass (Type: string) - Additional CSS class(es) to be added to a modal window template.

windowTemplateUrl (Type: string, Default: uib/template/modal/window.html) - A path to a template overriding modal's window template.

windowTopClass (Type: string) - CSS class(es) to be added to the top modal window.

Global defaults may be set for $uibModal via $uibModalProvider.options.

The open method returns a modal instance, an object with the following properties:

close(result) (Type: function) - Can be used to close a modal, passing a result.

dismiss(reason) (Type: function) - Can be used to dismiss a modal, passing a reason.

result (Type: promise) - Is resolved when a modal is closed and rejected when a modal is dismissed.

opened (Type: promise) - Is resolved when a modal gets opened after downloading content's template and resolving all variables.

closed (Type: promise) - Is resolved when a modal is closed and the animation completes.

rendered (Type: promise) - Is resolved when a modal is rendered.

The scope associated with modal's content is augmented with:

$close(result) (Type: function) - A method that can be used to close a modal, passing a result.

$dismiss(reason) (Type: function) - A method that can be used to dismiss a modal, passing a reason.

Those methods make it easy to close a modal window without a need to create a dedicated controller.

$uibUnscheduledDestruction - This event is fired if the $scope is destroyed via unexpected mechanism, such as it being passed in the modal options and a $route/$state transition occurs. The modal will also be dismissed.

modal.closing - This event is broadcast to the modal scope before the modal closes. If the listener calls preventDefault() on the event, then the modal will remain open. Also, the $close and $dismiss methods returns true if the event was executed. This event also includes a parameter for the result/reason and a boolean that indicates whether the modal is being closed (true) or dismissed.

If one wants to have the modal resolve using UI Router's pre-1.0 resolve mechanism, one can call $uibResolve.setResolver('$resolve') in the configuration phase of the application. One can also provide a custom resolver as well, as long as the signature conforms to UI Router's $resolve.

A lightweight pager directive that is focused on providing previous/next paging functionality

align C (Default: true) - Whether to align each link to the sides.

items-per-page $ C (Default: 10) - Maximum number of items per page. A value less than one indicates all items on one page.

next-text C (Default: Next ») - Text for Next button.

ng-disabled $ (Default: false) - Used to disable the pager component.

ng-model $ - Current page number. First page is 1.

num-pages $ readonly (Default: angular.noop) - An optional expression assigned the total number of pages to display.

previous-text C (Default: « Previous) - Text for Previous button.

template-url (Default: template/pagination/pager.html) - Override the template for the component with a custom provided template.

total-items $ - Total number of items in all pages.

A lightweight pagination directive that is focused on ... providing pagination & will take care of visualising a pagination bar and enable / disable buttons correctly!

boundary-links C (Default: false) - Whether to display First / Last buttons.

boundary-link-numbers $ C (Default: false) - Whether to always display the first and last page numbers. If max-size is smaller than the number of pages, then the first and last page numbers are still shown with ellipses in-between as necessary. NOTE: max-size refers to the center of the range. This option may add up to 2 more numbers on each side of the displayed range for the end value and what would be an ellipsis but is replaced by a number because it is sequential.

direction-links $ C (Default: true) - Whether to display Previous / Next buttons.

first-text C (Default: First) - Text for First button.

force-ellipses $ C (Default: false) - Also displays ellipses when rotate is true and max-size is smaller than the number of pages.

items-per-page $ C (Default: 10) - Maximum number of items per page. A value less than one indicates all items on one page.

last-text C (Default: Last) - Text for Last button.

max-size $ (Default: null) - Limit number for pagination size.

next-text C (Default: Next) - Text for Next button.

ng-change $ - This can be used to call a function whenever the page changes.

ng-disabled $ (Default: false) - Used to disable the pagination component.

ng-model $ - Current page number. First page is 1.

num-pages $ readonly (Default: angular.noop) - An optional expression assigned the total number of pages to display.

previous-text C (Default: Previous) - Text for Previous button.

rotate $ C (Default: true) - Whether to keep current page in the middle of the visible ones.

template-url (Default: uib/template/pagination/pagination.html) - Override the template for the component with a custom provided template

total-items $ - Total number of items in all pages.

A lightweight, extensible directive for fancy popover creation. The popover directive supports multiple placements, optional transition animation, and more.

Like the Bootstrap jQuery plugin, the popover requires the tooltip module.

Note to mobile developers: Please note that while popovers may work correctly on mobile devices (including tablets), we have made the decision to not officially support such a use-case because it does not make sense from a UX perspective.

There are three versions of the popover: uib-popover and uib-popover-template, and uib-tooltip-html:

All these settings are available for the three types of popovers.

popover-animation $ C (Default: true, Config: animation) - Should it fade in and out?

popover-append-to-body $ (Default: false) - Should the popover be appended to '$body' instead of the parent element?

popover-is-open (Default: false) - Whether to show the popover.

popover-placement C (Default: top, Config: placement) - Passing in 'auto' separated by a space before the placement will enable auto positioning, e.g: "auto bottom-left". The popover will attempt to position where it fits in the closest scrollable ancestor. Accepts:

popover-popup-close-delay C (Default: 0, Config: popupCloseDelay) - For how long should the popover remain open after the close trigger event?

popover-popup-delay C (Default: 0, Config: popupDelay) - Popup delay in milliseconds until it opens.

popover-title - A string to display as a fancy title.

popover-trigger (Default: mouseenter) - What should trigger a show of the popover? Supports a space separated list of event names (see below).

Note: To configure the tooltips, you need to do it on $uibTooltipProvider (also see below).

The following show triggers are supported out of the box, along with their provided hide triggers:

The outsideClick trigger will cause the popover to toggle on click, and hide when anything else is clicked.

For any non-supported value, the trigger will be used to both show and hide the popover. Using the 'none' trigger will disable the internal trigger(s), one can then use the popover-is-open attribute exclusively to show and hide the popover.

Through the $uibTooltipProvider, you can change the way tooltips and popovers behave by default; the attributes above always take precedence. The following methods are available:

setTriggers(obj) (Example: { 'openTrigger': 'closeTrigger' }) - Extends the default trigger mappings mentioned above with mappings of your own.

options(obj) - Provide a set of defaults for certain tooltip and popover attributes. Currently supports the ones with the C badge.

For Safari 7+ support, if you want to use focus popover-trigger, you need to use an anchor tag with a tab index. For example:

The $uibPosition service provides a set of DOM utilities used internally to absolute-position an element in relation to another element (tooltips, popovers, typeaheads etc...).

Takes a jQuery/jqLite element and converts it to a raw DOM element.

Parses a numeric style value to a number. Strips units and will return 0 for invalid (NaN) numbers.

Gets the closest positioned ancestor.

Calculates the browser scrollbar width and caches the result for future calls. Concept from the TWBS measureScrollbar() function in modal.js.

Gets the closest scrollable ancestor. Concept from the jQueryUI scrollParent.js.

element (Type: element) - The element to get the closest scrollable ancestor for.

includeHidden (Type: boolean, Default: false, optional) - Should scroll style of 'hidden' be considered.

A read-only equivalent of jQuery's position function, distance to closest positioned ancestor. Does not account for margins by default like jQuery's position.

element (Type: element) - The element to get the position for.

includeMargins (Type: boolean, Default: false, optional) - Should margins be accounted for.

An object with the following properties:

width (Type: number) - The width of the element.

height (Type: number) - The height of the element.

top (Type: number) - Distance to top edge of offset parent.

left (Type: number) - Distance to left edge of offset parent.

A read-only equivalent of jQuery's offset function, distance to viewport.

An object with the following properties:

width (Type: number) - The width of the element.

height (Type: number) - The height of the element.

top (Type: number) - Distance to top edge of the viewport.

left (Type: number) - Distance to left edge of the viewport.

Gets the elements available space relative to the closest scrollable ancestor. Accounts for padding, border, and scrollbar width. Right and bottom dimensions represent the distance to the respective edge of the viewport element, not the top and left edge. If the element edge extends beyond the viewport, a negative value will be reported.

element (Type: element) - The element to get the viewport offset for.

useDocument (Type: boolean, Default: false, optional) - Should the viewport be the document element instead of the first scrollable element.

includePadding (Type: boolean, Default: true, optional) - Should the padding on the viewport element be accounted for, default is true.

An object with the following properties:

top (Type: number) - Distance to top content edge of the viewport.

bottom (Type: number) - Distance to bottom content edge of the viewport.

left (Type: number) - Distance to left content edge of the viewport.

right (Type: number) - Distance to right content edge of the viewport.

Gets an array of placement values parsed from a placement string. Along with the 'auto' indicator, supported placement strings are:

A placement string with an 'auto' indicator is expected to be space separated from the placement, i.e: 'auto bottom-left'. If the primary and secondary placement values do not match 'top, bottom, left, right' then 'top' will be the primary placement and 'center' will be the secondary placement. If 'auto' is passed, true will be returned as the 3rd value of the array.

An array with the following values:

[0] (Type: string) - The primary placement.

[1] (Type: string) - The secondary placement.

[2] (Type: boolean) - Is auto place enabled.

Gets gets coordinates for an element to be positioned relative to another element.

hostElement (Type: element) - The element to position against.

targetElement (Type: element) - The element to position.

placement (Type: string, Default: top, optional) - The placement for the target element. See the parsePlacement() function for available options. If 'auto' placement is used, the viewportOffset() function is used to decide where the targetElement will fit.

appendToBody (Type: boolean, Default: false, optional) - Should the coordinates be cacluated from the body element.

An object with the following properties:

top (Type: number) - The targetElement top value.

left (Type: number) - The targetElement left value.

right (Type: number) - The resolved placement with 'auto' removed.

Positions the tooltip and popover arrow elements when using placement options beyond the standard top, left, bottom, or right.

element (Type: element) - The element to position the arrow element for.

placement (Type: string) - The placement for the element.

A progress bar directive that is focused on providing feedback on the progress of a workflow or action.

It supports multiple (stacked) <uib-bar> into the same <uib-progress> element or a single <uib-progressbar> element with optional max attribute and transition animations.

value $ - The current value of progress completed.

type (Default: null) - Bootstrap style type. Possible values are 'success', 'info', 'warning', and, 'error' to use Bootstrap's pre-existing styling, or any desired custom suffix.

max $ C (Default: 100) - A number that specifies the total value of bars that is required.

animate $ C (Default: true) - Whether bars use transitions to achieve the width change.

title (Default: progressbar) - Title to use as label (for accessibility).

max $ C (Default: 100) - A number that specifies the total value of bars that is required.

animate $ C (Default: true) - Whether bars use transitions to achieve the width change.

title (Default: progressbar) - Title to use as label (for accessibility).

value $ - The current value of progress completed.

type (Default: null) - Bootstrap style type. Possible values are 'success', 'info', 'warning', and, 'error' to use Bootstrap's pre-existing styling, or any desired custom suffix.

title (Default: progressbar) - Title to use as label (for accessibility).

Rating directive that will take care of visualising a star rating bar.

max $ C (Default: 5) - Changes the number of icons.

ng-model $ - The current rate.

on-hover(value) $ - An optional expression called when user's mouse is over a particular icon.

on-leave() $ - An optional expression called when user's mouse leaves the control altogether.

rating-states $ (Default: null) - An array of objects defining properties for all icons. In default template, stateOn & stateOff property is used to specify the icon's class.

readonly $ (Default: false) - Prevent user's interaction.

titles $ C (Default: ['one', 'two', 'three', 'four', 'five']`) - An array of strings defining titles for all icons.

state-off $ C (Default: null) - A variable used in the template to specify the state for unselected icons.

state-on $ C (Default: null) - A variable used in the template to specify the state (class, src, etc) for selected icons.

Select a tab by setting active binding to true:

Select second tab Select third tab

Enable / Disable third tab

AngularJS version of the tabs directive.

justified $ (Default: false) - Whether tabs fill the container and have a consistent width.

type (Defaults: tabs) - Navigation type. Possible values are 'tabs' and 'pills'.

vertical $ (Default: false) - Whether tabs appear vertically stacked.

active $ (Default: false) - Whether tab is currently selected.

deselect() $ - An optional expression called when tab is deactivated.

disable $ (Default: false) - Whether tab is clickable and can be activated.

heading - Heading text.

select() $ - An optional expression called when tab is activated.

Instead of the heading attribute on the uib-tabset, you can use an uib-tab-heading element inside a tabset that will be used as the tabset's header. There you can use HTML as well.

To use clickable elements within the tab, you have override the tab template to use div elements instead of anchor elements, and replicate the desired styles from Bootstrap's CSS. This is due to browsers interpreting anchor elements as the target of any click event, which triggers routing when certain elements such as buttons are nested inside the anchor element.

A lightweight & configurable timepicker directive.

arrowkeys $ C (Default: true) - Whether user can use up/down arrow keys inside the hours & minutes input to increase or decrease its values.

hour-step $ C (Default: 1) - Number of hours to increase or decrease when using a button.

max $ (Default: undefined) - Maximum time a user can select.

meridians $ C (Default: null) - Meridian labels based on locale. To override you must supply an array like ['AM', 'PM'].

min $ (Default: undefined) - Minimum time a user can select

minute-step $ C (Default: 1) - Number of minutes to increase or decrease when using a button.

mousewheel $ C (Default: true) - Whether user can scroll inside the hours & minutes input to increase or decrease its values.

ng-disabled $ (Default: false) - Whether or not to disable the component.

ng-model $ - Date object that provides the time state.

readonly-input $ C (Default: false) - Whether user can type inside the hours & minutes input.

second-step $ C (Default: 1) - Number of seconds to increase or decrease when using a button.

show-meridian $ C (Default: true) - Whether to display 12H or 24H mode.

show-seconds $ C (Default: false) - Show seconds input.

show-spinners $ C (Default: true) - Show spinner arrows above and below the inputs.

tabindex (Defaults: 0) - Sets tabindex for each control in the timepicker.

template-url C (Defaults: uib/template/timepicker/timepicker.html) - Add the ability to override the template used on the component.

If the model value is updated (i.e. via Date.prototype.setDate), you must update the model value by breaking the reference by modelValue = new Date(modelValue) in order to have the timepicker update.

Pellentesque {{dynamicTooltipText}}, sit amet venenatis urna cursus eget nunc scelerisque viverra mauris, in aliquam. Tincidunt lobortis feugiat vivamus at fading eget arcu dictum varius duis at consectetur lorem. Vitae elementum curabitur show delay nunc sed velit dignissim sodales ut eu sem integer vitae. Turpis egestas hide delay pharetra convallis posuere morbi leo urna, Custom template at elementum eu, facilisis sed odio morbi quis commodo odio.

I can even contain HTML. Check me out!

I can have a custom class. Check me out!

A lightweight, extensible directive for fancy tooltip creation. The tooltip directive supports multiple placements, optional transition animation, and more.

Note to mobile developers: Please note that while tooltips may work correctly on mobile devices (including tablets), we have made the decision to not officially support such a use-case because it does not make sense from a UX perspective.

There are three versions of the tooltip: uib-tooltip, uib-tooltip-template, and uib-tooltip-html:

All these settings are available for the three types of tooltips.

tooltip-animation $ C (Default: true, Config: animation) - Should it fade in and out?

tooltip-append-to-body $ (Default: false) - Should the tooltip be appended to '$body' instead of the parent element?

tooltip-class - Custom class to be applied to the tooltip.

tooltip-enable $ (Default: true) - Is it enabled? It will enable or disable the configured tooltip-trigger.

tooltip-is-open (Default: false) - Whether to show the tooltip.

tooltip-placement C (Default: top, Config: placement) - Passing in 'auto' separated by a space before the placement will enable auto positioning, e.g: "auto bottom-left". The tooltip will attempt to position where it fits in the closest scrollable ancestor. Accepts:

tooltip-popup-close-delay C (Default: 0, Config: popupCloseDelay) - For how long should the tooltip remain open after the close trigger event?

tooltip-popup-delay C (Default: 0, Config: popupDelay) - Popup delay in milliseconds until it opens.

tooltip-trigger (Default: mouseenter) - What should trigger a show of the tooltip? Supports a space separated list of event names (see below).

Note: To configure the tooltips, you need to do it on $uibTooltipProvider (also see below).

The following show triggers are supported out of the box, along with their provided hide triggers:

The outsideClick trigger will cause the tooltip to toggle on click, and hide when anything else is clicked.

For any non-supported value, the trigger will be used to both show and hide the tooltip. Using the 'none' trigger will disable the internal trigger(s), one can then use the tooltip-is-open attribute exclusively to show and hide the tooltip.

Through the $uibTooltipProvider, you can change the way tooltips and popovers behave by default; the attributes above always take precedence. The following methods are available:

setTriggers(obj) (Example: { 'openTrigger': 'closeTrigger' }) - Extends the default trigger mappings mentioned above with mappings of your own.

options(obj) - Provide a set of defaults for certain tooltip and popover attributes. Currently supports the ones with the C badge.

For Safari 7+ support, if you want to use the focus tooltip-trigger, you need to use an anchor tag with a tab index. For example:

Typeahead is a AngularJS version of Bootstrap v2's typeahead plugin. This directive can be used to quickly create elegant typeaheads with any form text input.

It is very well integrated into AngularJS as it uses a subset of the select directive syntax, which is very flexible. Supported expressions are:

The sourceArray expression can use a special $viewValue variable that corresponds to the value entered inside the input.

This directive works with promises, meaning you can retrieve matches using the $http service with minimal effort.

ng-model $ - Assignable angular expression to data-bind to.

ng-model-options $ - Options for ng-model (see ng-model-options directive). Currently supports the debounce and getterSetter options.

typeahead-append-to $ (Default: null) - Should the typeahead popup be appended to an element instead of the parent element?

typeahead-append-to-body $ (Default: false) - Should the typeahead popup be appended to $body instead of the parent element?

typeahead-editable $ (Default: true) - Should it restrict model values to the ones selected from the popup only?

typeahead-focus-first $ (Default: true) - Should the first match automatically be focused as you type?

typeahead-focus-on-select (Default: true) - On selection, focus the input element the typeahead directive is associated with.

typeahead-input-formatter (Default: undefined) - Format the ng-model result after selection.

typeahead-is-open $ (Default: angular.noop) - Binding to a variable that indicates if the dropdown is open.

typeahead-loading $ (Default: angular.noop) - Binding to a variable that indicates if matches are being retrieved asynchronously.

typeahead-min-length $ (Default: 1) - Minimal no of characters that needs to be entered before typeahead kicks-in. Must be greater than or equal to 0.

typeahead-no-results $ (Default: angular.noop) - Binding to a variable that indicates if no matching results were found.

typeahead-on-select($item, $model, $label, $event) $ (Default: null) - A callback executed when a match is selected. $event can be undefined if selection not triggered from a user event.

typeahead-popup-template-url (Default: uib/template/typeahead/typeahead-popup.html) - Set custom popup template.

typeahead-select-on-blur $ (Default: false) - On blur, select the currently highlighted match.

typeahead-select-on-exact $ (Default: false) - Should it automatically select an item when there is one option that exactly matches the user input?

typeahead-show-hint $ (Default: false) - Should input show hint that matches the first option?

typeahead-template-url (Default: uib/template/typeahead/typeahead-match.html) - Set custom item template.

typeahead-wait-ms $ (Default: 0) - Minimal wait time after last character typed before typeahead kicks-in.

uib-typeahead $ - Comprehension Angular expression (see select directive).

**Examples:**

Example 1 (unknown):

```unknown
angular.module('myModule', ['ui.bootstrap']);
```

Example 2 (css):

```css
.nav,
.pagination,
.carousel,
.panel-title a {
  cursor: pointer;
}
```

Example 3 (html):

```html
<div ng-controller="AccordionDemoCtrl">
  <script
    type="text/ng-template"
    id="group-template.html">
    <div class="panel {{panelClass || 'panel-default'}}">
      <div class="panel-heading">
        <h4 class="panel-title" style="color:#fa39c3">
          <a href tabindex="0" class="accordion-toggle" ng-click="toggleOpen()" uib-accordion-transclude="heading"><span
            ng-class="{'text-muted': isDisabled}">{{heading}}</span></a>
        </h4>
      </div>
      <div class="panel-collapse collapse" uib-collapse="!isOpen">
        <div class="panel-body" style="text-align: right" ng-transclude></div>
      </div>
    </div>
  </script>

  <p>
    <button
      type="button"
      class="btn btn-default btn-sm"
      ng-click="status.open = !status.open">
      Toggle last panel
    </button>
    <button
      type="button"
      class="btn btn-default btn-sm"
      ng-click="status.isFirstDisabled = ! status.isFirstDisabled">
      Enable / Disable first panel
    </button>
  </p>

  <div class="checkbox">
    <label>
      <input
        type="checkbox"
        ng-model="oneAtATime" />
      Open only one at a time
    </label>
  </div>
  <uib-accordion close-others="oneAtATime">
    <uib-accordion-group
      heading="Static Header, initially expanded"
      is-open="status.isFirstOpen"
      is-disabled="status.isFirstDisabled">
      This content is straight in the template.
    </uib-accordion-group>
    <uib-accordion-group
      heading="{{group.title}}"
      ng-repeat="group in groups">
      {{group.content}}
    </uib-accordion-group>
    <uib-accordion-group heading="Dynamic Body Content">
      <p>The body of the uib-accordion group grows to fit the contents</p>
      <button
        type="button"
        class="btn btn-default btn-sm"
        ng-click="addItem()">
        Add Item
      </button>
      <div ng-repeat="item in items">{{item}}</div>
    </uib-accordion-group>
    <uib-accordion-group
      heading="Custom template"
      template-url="group-template.html">
      Hello
    </uib-accordion-group>
    <uib-accordion-group
      heading="Delete account"
      panel-class="panel-danger">
      <p>Please, to delete your account, click the button below</p>
      <button class="btn btn-danger">Delete</button>
    </uib-accordion-group>
    <uib-accordion-group is-open="status.open">
      <uib-accordion-heading>
        I can have markup, too!
        <i
          class="pull-right glyphicon"
          ng-class="{'glyphicon-chevron-down': status.open, 'glyphicon-chevron-right': !status.open}"></i>
      </uib-accordion-heading>
      This is just some content to illustrate fancy headings.
    </uib-accordion-group>
  </uib-accordion>
</div>
```

Example 4 (gdscript):

```gdscript
angular.module('ui.bootstrap.demo').controller('AccordionDemoCtrl', function ($scope) {
  $scope.oneAtATime = true;

  $scope.groups = [
    {
      title: 'Dynamic Group Header - 1',
      content: 'Dynamic Group Body - 1'
    },
    {
      title: 'Dynamic Group Header - 2',
      content: 'Dynamic Group Body - 2'
    }
  ];

  $scope.items = ['Item 1', 'Item 2', 'Item 3'];

  $scope.addItem = function() {
    var newItemNo = $scope.items.length + 1;
    $scope.items.push('Item ' + newItemNo);
  };

  $scope.status = {
    isFirstOpen: true,
    isFirstDisabled: false
  };
});
```

---
